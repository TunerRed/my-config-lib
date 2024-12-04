FROM hxsoong/kylin:v10-sp2
MAINTAINER tunerred
WORKDIR /tidb/
VOLUME ["/tidb/tiup/data/smartoffice","/tidb/tiup/logs"]
EXPOSE 4000 3930 3000 2379

RUN yum install -y wget expect vim \
	&& rm -f /etc/localtime \
	&& ln -sv /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
	&& echo "Asia/Shanghai" > /etc/timezone
RUN curl --proto '=https' --tlsv1.2 -sSf https://tiup-mirrors.pingcap.com/install.sh | sh \
	&& ln -s /root/.tiup/ /tidb/tiup
ENV PATH=/root/.tiup/bin:$PATH
RUN tiup install playground:v1.16.1 \
	&& tiup install prometheus:v6.5.3 \
	&& tiup install grafana:v6.5.3 \
	&& tiup install tiflash:v6.5.3 \
	&& tiup install pd:v6.5.3 \
	&& tiup install tikv:v6.5.3 \
	&& tiup install tidb:v6.5.3

entrypoint tiup playground v6.5.3 --tag mytidb --host 0.0.0.0
