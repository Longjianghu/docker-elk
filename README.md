### 项目说明

官网地址： https://www.docker.elastic.co。

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

docker build -t elasticsearch:642 ./app/elasticsearch/

### 运行方法

Elasticsearch

docker run --name elasticsearch -p 9200:9200 -p 9300:9300 -v /data/var/lib/elasticsearch/master:/usr/share/elasticsearch/data -v /data/var/etc/elasticsearch/master.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /data/var/etc/elasticsearch/IKAnalyzer.cfg.xml:/usr/share/elasticsearch/config/analysis-ik/IKAnalyzer.cfg.xml --ulimit memlock=-1 -d elasticsearch:642
		
Kibana:

docker run --name kibana -p 5601:5601 -v /data/var/etc/kibana/kibana.yml:/usr/share/kibana/config/kibana.yml -d kibana:6.4.2

Logstash:

docker run --name logstash -d logstash:6.4.2

Filebeat：

docker run --name filebeat -v /data/var/etc/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /data/var/etc/filebeat/prospectors.d:/usr/share/filebeat/prospectors.d -d filebeat:6.4.2
