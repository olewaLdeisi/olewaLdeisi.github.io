## 1. 使用thrift做rpc
windows [下载地址](http://www.apache.org/dyn/closer.cgi?path=/thrift/0.10.0)
下载后随便放到一个目录比如 `C://Thrift`，在环境变量Path中加入 `C://Thrift`;

### 1.1. java导入依赖
```
<dependency>
    <groupId>org.apache.thrift</groupId>
    <artifactId>libthrift</artifactId>
    <version>0.10.0</version>
</dependency>
```

### 1.2. python导入依赖
windows版：  
[官网源码](https://github.com/apache/thrift/archive/0.10.0.zip)下载，解压后进入`thrift-0.10.0/lib/py`执行：  
> python setup.py install

linux版:

### 1.3. 编写thrift文件 `analyze_service.thrift`
```
service AnalyzeService {
    string analyzeImage(1:string imageName)
}
```
打开cmd，执行
> thrift --gen py analyze_service.thrift  
> thrift --gen java analyze_service.thrift

### 1.4. python做服务端
```
"""
-------------------------------------------------
   Author :        lin
   date：          2019/8/24 22:14
-------------------------------------------------
"""
__author__ = 'lin'


import torch
import os
from analyze_service import AnalyzeService

from thrift.transport import TSocket
from thrift.transport import TTransport
from thrift.protocol import TBinaryProtocol
from thrift.server import TServer
from net.classify import load_net, imgPathToTensor, classify

__HOST = '172.18.0.4'
__PORT = 3049


model = load_net()


class AnalyzeImageHandler(object):
    def analyzeImage(self, imageName):
        '''
        :param imageName: 一张或多张图片路径， 分号隔开
        :return: 分析结果
        '''
        for index, img in enumerate(imageName):
            if index == 0:
                inputs = imgPathToTensor(img)
            else:
                inputs = torch.cat((inputs, imgPathToTensor(img)), 0)
        return classify(inputs, model)

if __name__ == '__main__':
    print("===================== start server =====================")
    handler = AnalyzeImageHandler()

    processor = AnalyzeService.Processor(handler)
    transport = TSocket.TServerSocket(__HOST, __PORT)
    tfactory = TTransport.TBufferedTransportFactory()
    pfactory = TBinaryProtocol.TBinaryProtocolFactory()

    rpcServer = TServer.TForkingServer(processor, transport, tfactory, pfactory)
    rpcServer.serve()

```

### 1.5. java做客户端
```
package cn.gpnu.qtyy.service;

import org.apache.thrift.TException;
import org.apache.thrift.protocol.TBinaryProtocol;
import org.apache.thrift.protocol.TProtocol;
import org.apache.thrift.transport.TSocket;
import org.apache.thrift.transport.TTransport;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import java.util.List;

/**
 * cn.gpnu.qtyy.service.ThriftClient class
 * <p>
 *
 * </p>
 *
 * @author Lin Xiaopeng
 * @date 2019/8/24
 */
@Component
public class ThriftClient {
    @Value("${spring.pythonserver.host}")
    private String host;

    @Value("${spring.pythonserver.port}")
    private Integer port;

    public String startClient(List<String> imageName) {
        TTransport transport;
        String result = "";
        try {
            transport = new TSocket(host, port);
            TProtocol protocol = new TBinaryProtocol(transport);
            AnalyzeService.Client client = new AnalyzeService.Client(protocol);
            transport.open();
            result = client.analyzeImage(imageName);
            transport.close();
            return result;
        } catch (TException e) {
            e.printStackTrace();
            return e.getMessage();
        }
    }
}
```

## 2. 使用docker

### 2.1. pom.xml 添加依赖
```
<properties>
    <docker.image.prefix>springboot</docker.image.prefix>
</properties>
```
```
<plugin>
    <groupId>com.spotify</groupId>
    <artifactId>docker-maven-plugin</artifactId>
    <version>1.0.0</version>
    <configuration>
        <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
        <dockerDirectory>src/main/docker</dockerDirectory>
        <resources>
            <resource>
                <targetPath>/</targetPath>
                <directory>${project.build.directory}</directory>
                <include>${project.build.finalName}.jar</include>
            </resource>
        </resources>
    </configuration>
</plugin>
```

### 2.2. 编辑Dockerfile
```
FROM java:8
EXPOSE 3048
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/data/qtyy.jar"]
```

```
FROM python:3.7
EXPOSE 3049
ADD ./requirements.txt /code/requirements.txt
RUN pip install numpy
RUN pip install --pre torch torchvision -f https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html
RUN pip install thrift==0.10.0
RUN pip install dropblock
ENTRYPOINT ["python", "/code/gen-py/main.py"]
```

### 2.3. 构建镜像
进入Drockerfile所在目录
> docker build -t springboot_qtyy_images .

> docker build -t deeplearning_images .

### 2.4. 创建并启动容器
>  docker run --network bridge --name springboot_qtyy -it -v /var/www/target:/data -d -p 3048:3048 springboot_qtyy_images

>  docker run --network bridge --name deeplearning -it -v /var/www/deeplearning:/code -d -p 3049:3049 deeplearning_images

### 2.5. 创建一个桥接网络(可选)
下面的localNet是网络名字,可自行修改;关于192.168.0.0这个子网,也可以自行定义.
默认按照下面的命令,执行后将可以通过192.168.0.1访问宿主机.
> docker network create -d bridge --subnet 192.168.0.0/24 --gateway 192.168.0.1 localNet
