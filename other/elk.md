#### Elasticsearch + Kibana + X-Pack 

- Elasticsearch、x-pack、Kibana 的版本号要一致
- Elasticsearch 和 Kibana 均要安装x-pack
	- 安装x-pack有两种方式(用es举例子，kibana同)
		1. `bin/elasticsearch-plugin install x-pack`
		2. `bin/elasticsearch-plugin install file:/file-path-of-x-pack.zip(绝对路径)`
- 取消x-pack的用户认证
	1. 配置`elasticsearch.yml`
	`xpack.security.enabled: false`
	
	2. 配置`kibana.yml`
	`elasticsearch.ssl.verificationMode: none`
	`elasticsearch.requestHeadersWhitelist: []`

---------------------------
#### ES、X-Pack、Kibana 5.6.3 搭建集群并监控(非docker、同一台机器)

1. 去官网下载`Elasticsearch`、`X-Pack`、`Kibana` 的包，注意`版本号要一致`
2. 解压两份`Elasticsearch`，分别安装`X-Pack`
3. 配置`elasticsearch.yml`

第一个`es`的`yml`配置：

``` 
cluster.name: my-es # 名字要一致
node.name: es1
node.master: true
node.data: true
network.host: 0.0.0.0
http.port: 9200
transport.tcp.port: 9300
discovery.zen.ping.unicast.hosts: ["127.0.0.1:9300", "127.0.0.1:9301"] # 5.4.3就不写:port
discovery.zen.minimum_master_nodes: 1
discovery.zen.ping_timeout: 300s
xpack.security.enabled: false
```

第二个`es`的`yml`配置：


``` 
cluster.name: my-es # 名字要一致
node.name: es2
node.master: true
node.data: true
network.host: 0.0.0.0
http.port: 9201
transport.tcp.port: 9301
discovery.zen.ping.unicast.hosts: ["127.0.0.1:9300", "127.0.0.1:9301"] # 5.4.3就不写:port
discovery.zen.minimum_master_nodes: 1
discovery.zen.ping_timeout: 300s
xpack.security.enabled: false
```

4. 配置`kibana.yml`


``` 
elasticsearch.ssl.verificationMode: none
elasticsearch.requestHeadersWhitelist: []

```
5. 用`bin/elasticsearch`分别启动两个`es`
6. 用`bin/kibana`启动`kibana`
7. 访问`localhost:5601`
8.安装env1上(腾讯云/mnt/kibana/kibana-5.4.3-linux-x86_64/bin/../node/bin/node --no-warnings /mnt/kibana/kibana-5.4.3-linux-x86_64/bin/../src/cli)
暂时取消kibana网页访问，如果要访问，先启动在env1上启动就可以访问了，主要没有验证->数据丢失原因排查

---------------------------
### Docker 镜像构建方法
`docker build -t repository:tagname path-of-Dockerfile(相对路径就行)`
构建完后用`docker push repository:tagname`提交镜像到服务器



###  _!!#ff0000注意：各个版本之间有差异，具体要仔细阅读官方文档!!_