FROM elasticsearch:6.7.2

MAINTAINER Longjianghu <215241062@qq.com>

# 安装IK分词 https://github.com/medcl/elasticsearch-analysis-ik
# 安装拼音 https://github.com/medcl/elasticsearch-analysis-pinyin

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install -b https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.7.2/elasticsearch-analysis-ik-6.7.2.zip

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install -b https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v6.7.2/elasticsearch-analysis-pinyin-6.7.2.zip