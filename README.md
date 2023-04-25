# nacos-coredns-plugin [中文](./README_CN.md) #
This project provides a **DNS-F** client based on [CoreDNS](https://coredns.io/), which can help export those registed services on Nacos as DNS domain. **DNS-F** client is a dedicated agent process(side car) beside the application's process to foward the service discovery DNS domain query request to Nacos. 

## Quic Start
To build and run nacos coredns plugin, the OS must be Linux or Mac. And also, make sure your nacos version is 2.0 or higher and golang version is 1.17 or higher.  And golang environments(GOPATH,GOROOT,GOHOME) must be configured correctly. Because it needs to support the gRPC connection feature  of the nacos2.x version  and  the go mod function.

### Build
```
git clone https://github.com/nacos-group/nacos-coredns-plugin.git 
cp nacos-coredns-plugin/bin/build.sh ~/
cd ~/
sh build.sh
```
### Configuration
To run nacos coredns plugin, you need a configuration file. A possible file may be as bellow:
```
. {
    log
    nacos {
        nacos_namespaceId public
        nacos_server_host 127.0.0.1:8848
   }
   forward . /etc/resolv.conf
 }
```
* forward: domain names those not registered in nacos will be forwarded to upstream.
* nacos_namespaceId: nacos namespaceId, defalut is public.
* nacos_server_host: Ip and Port of nacos server, seperated by comma if there are two or more nacos servers

### Run
* Firstly, you need to deploy nacos server. [Here](https://github.com/alibaba/nacos)
* Secondly, register service on nacos.
* Then run ```$GOPATH/src/coredns/coredns -conf $path_to_corefile -dns.port $dns_port```
![image](https://cdn.nlark.com/yuque/0/2022/png/29425667/1663504581023-95437fee-0e3d-4b6a-851c-44a352dedd81.png)

### Test
dig $nacos_service_name @127.0.0.1 -p $dns_port

![image](https://cdn.nlark.com/yuque/0/2022/png/29425667/1663504588231-341b38fe-da55-41eb-a24b-e3752b86faa4.png)
