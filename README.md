# nacos-coredns-plugin

> fork from https://github.com/nacos-group/nacos-coredns-plugin add coredns latest version support and add username & password support 


## setup

* plugin.cfg (order is important)

```code
kubernetes:kubernetes
nacos:github.com/rongfengliang/coredns-nacos
file:file
auto:auto
secondary:secondary
etcd:etcd
```

* run build

```code
go generate   
make
```

## config

> for security must provide nacos_username & nacos_password

```code
. {
    debug
    log
    nacos {
        nacos_namespaceId public
        nacos_server_host xxxx:8848
        nacos_username xxx
        nacos_password xxxx
   }
   forward com 8.8.8.8
}
```


## Some Notes

* for go 1.24.3 

```code
coredns deps https://github.com/ebitengine/purego should upgrade to latest version
```
