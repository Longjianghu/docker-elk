### 项目说明

更详细的使用说明请看这是：https://www.docker.elastic.co/ 请注意：如果内存过小将无法启动(所有镜像均来自于官方 https://www.docker.elastic.co/ ，因为下载速度慢被转移作者转移到了docker官方仓库)。

### 安装 Docker

curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

usermod -aG docker  root

systemctl start docker

### 配置加速器

curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://8145ad9d.m.daocloud.io

### 安装 Docker-Compose

yum -y install epel-release python-pip

pip install docker-compose

### 构建容器

docker build -t elasticsearch:642 ./app/elasticsearch/

### 运行方法

Elasticsearch:

docker run --name elasticsearch642 -p 9200:9200 -p 9300:9300 -v /data/var/lib/elasticsearch:/usr/share/elasticsearch/data -v /data/var/etc/elasticsearch/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /data/var/etc/elasticsearch/IKAnalyzer.cfg.xml:/usr/share/elasticsearch/config/analysis-ik/IKAnalyzer.cfg.xml -d elasticsearch:642

Kibana:

docker run --name kibana642 -p 5601:5601 -v /data/var/etc/kibana/kibana.yml:/usr/share/kibana/config/kibana.yml -d longjianghu/kibana:6.4.2

Logstash:

docker run --name logstash642 -d longjianghu/logstash:6.4.2

Filebeat：

docker run --name filebeat642 -v /data/var/etc/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /data/var/etc/filebeat/prospectors.d:/usr/share/filebeat/prospectors.d -d longjianghu/filebeat:6.4.2

Elasticsearch HQ(通过 web 界面管理 Elasticsearch):

docker run --name elasticsearch-hq -p 5000:5000 -e HQ_DEFAULT_URL=http://172.17.0.1:9200 -d elastichq/elasticsearch-hq
