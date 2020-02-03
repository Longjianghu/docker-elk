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

yum -y install epel-release python-pip

pip install docker-compose

### 构建容器

docker build -t longjianghu/elasticsearch:7.1.1 ./app/elasticsearch/

### 运行方法

Elasticsearch

由于 Elasticsearch7版本自带 x-pack 安全认证插件,配置文件默认已经启用，如不需要请自行调整配置参数。

docker run --name elasticsearch -p 9200:9200 -p 9300:9300 -v /data/var/lib/elasticsearch/master:/usr/share/elasticsearch/data -v /data/var/etc/elasticsearch/master.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /data/var/etc/elasticsearch/IKAnalyzer.cfg.xml:/usr/share/elasticsearch/config/analysis-ik/IKAnalyzer.cfg.xml -e ES_JAVA_OPTS="-Xms1g -Xmx1g" --ulimit memlock=-1:-1 -d longjianghu/elasticsearch:7.1.1

设置密码:

auto:自动生成 interactive:手动配置

docker exec -it elasticsearch /usr/share/elasticsearch/bin/elasticsearch-setup-passwords auto

Kibana:

docker run --name kibana -p 5601:5601 -v /data/var/etc/kibana.yml:/usr/share/kibana/config/kibana.yml -d kibana:7.1.1

Logstash:

docker run --name logstash -d logstash:7.1.1

Filebeat:

docker run --name filebeat -v /data/var/etc/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /data/var/etc/filebeat/prospectors.d:/usr/share/filebeat/prospectors.d -d filebeat:7.1.1
