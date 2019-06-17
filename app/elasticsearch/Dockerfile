FROM docker.elastic.co/elasticsearch/elasticsearch:7.1.1

MAINTAINER Longjianghu <215241062@qq.com>

# 安装IK分词 https://github.com/medcl/elasticsearch-analysis-ik
# 安装拼音 https://github.com/medcl/elasticsearch-analysis-pinyin

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install -b https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.1.1/elasticsearch-analysis-ik-7.1.1.zip 
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install -b https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v7.1.1/elasticsearch-analysis-pinyin-7.1.1.zip  
