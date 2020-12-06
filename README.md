### 项目说明

官网地址： https://www.docker.elastic.co

参数配置:

https://www.elastic.co/guide/en/elasticsearch/reference/current/important-settings.html

https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

### 安装 Docker

curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

usermod -aG docker  root

systemctl start docker

### 配置加速器

curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s https://registry.docker-cn.com

### 安装 Docker-Compose

curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

chmod a+x /usr/local/bin/docker-compose

### 构建容器

docker build -t longjianghu/elasticsearch:7.9.3 ./app/elasticsearch/

### 运行方法

Elasticsearch

由于 Elasticsearch7版本自带 x-pack 安全认证插件,配置文件默认已经启用，如不需要请自行调整配置参数。

docker run --name elasticsearch -p 9200:9200 -p 9300:9300 -v /data/var/lib/elasticsearch:/usr/share/elasticsearch/data -v /data/var/etc/elasticsearch/master.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /data/var/etc/elasticsearch/IKAnalyzer.cfg.xml:/usr/share/elasticsearch/config/analysis-ik/IKAnalyzer.cfg.xml -e "bootstrap.memory_lock=true" -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" --ulimit memlock=-1:-1 --ulimit nofile=65535:65535 -d longjianghu/elasticsearch:7.9.3

> https://www.elastic.co/guide/en/elasticsearch/reference/7.9/docker.html

设置密码:

auto:自动生成 interactive:手动配置

docker exec -it elasticsearch /usr/share/elasticsearch/bin/elasticsearch-setup-passwords auto

Kibana:

docker run --name kibana -p 5601:5601 -v /data/var/etc/kibana.yml:/usr/share/kibana/config/kibana.yml -d kibana:7.9.3

> https://www.elastic.co/guide/en/kibana/7.9/docker.html

Logstash:

docker run --name logstash -v -v /data/var/etc/logstash.yml:/usr/share/logstash/config/logstash.yml -d logstash:7.9.3

> https://www.elastic.co/guide/en/logstash/7.9/docker-config.html

Filebeat:

docker run --name filebeat -v /data/var/etc/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /data/var/etc/filebeat/modules.d:/usr/share/filebeat/modules.d -d elastic/filebeat:7.9.3

> https://www.elastic.co/guide/en/beats/filebeat/7.9/running-on-docker.html
