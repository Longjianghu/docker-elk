### 项目说明

当前项目仅用于学习目的，请勿用于生产环境。

### 安装 Docker

curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

usermod -aG docker  root

systemctl start docker

### 配置加速器

curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://8145ad9d.m.daocloud.io

### 安装 Docker-Compose

yum -y install epel-release python-pip

pip install docker-compose

### 更换 Composer 镜像

composer config -g repo.packagist composer https://packagist.phpcomposer.com

### 构建容器

docker build -t docker-es:6.3 ./app/elasticsearch/

### 运行方法

Elasticsearch:

docker run --name docker-es -p 9200:9200 -p 9300:9300 -v /data/var/lib/elasticsearch:/usr/share/elasticsearch/data -v /data/var/etc/elasticsearch/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /data/var/etc/elasticsearch/IKAnalyzer.cfg.xml:/usr/share/elasticsearch/config/analysis-ik/IKAnalyzer.cfg.xml -d docker-es:6.3

Kibana:

docker run --name docker-kibana -p 5601:5601 -e ELASTICSEARCH_URL=http://172.17.0.1:9200 -d docker.elastic.co/kibana/kibana:6.3.0

Logstash:

docker run --name docker-logstash -d docker.elastic.co/logstash/logstash:6.3.0

Filebeat：

docker run --name docker-filebeat -v /data/var/etc/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /data/var/etc/filebeat/prospectors.d:/usr/share/filebeat/prospectors.d -d docker.elastic.co/beats/filebeat:6.3.0