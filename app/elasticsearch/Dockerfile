FROM elasticsearch:7.9.3

MAINTAINER Longjianghu <215241062@qq.com>

# 安装扩展
# IK分词 https://github.com/medcl/elasticsearch-analysis-ik
# 拼音 https://github.com/medcl/elasticsearch-analysis-pinyin

COPY ./src/* /tmp/

RUN set -xe \
	&& ./bin/elasticsearch-plugin install -b file:///tmp/elasticsearch-analysis-ik-7.9.3.zip \
	&& ./bin/elasticsearch-plugin install -b file:///tmp/elasticsearch-analysis-pinyin-7.9.3.zip \
	&& rm /tmp/* -rf