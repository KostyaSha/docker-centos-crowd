FROM centos:centos7
MAINTAINER kanstantsin.sha@gmail.com

RUN yum -y update; yum clean all
RUN yum -y install epel-release; yum clean all
#tools for debug
RUN yum -y install wget lsof nmap
# java itself
RUN yum -y install java-1.8.0-openjdk-devel

ENV PRODUCT=atlassian-crowd
ENV PRODUCT_VERSION=2.8.3
ENV PRODUCT_HOME=/opt/${PRODUCT}

RUN useradd "$PRODUCT"

RUN mkdir -p "$PRODUCT_HOME" && chown ${PRODUCT}. -R "$PRODUCT_HOME"

USER "${PRODUCT}"
WORKDIR /home/${PRODUCT}

RUN wget --progress=dot:giga https://www.atlassian.com/software/crowd/downloads/binary/${PRODUCT}-${PRODUCT_VERSION}.tar.gz
RUN tar xf ${PRODUCT}-${PRODUCT_VERSION}.tar.gz
RUN rm ${PRODUCT}-${PRODUCT_VERSION}.tar.gz

RUN echo "crowd.home=$PRODUCT_HOME" > ${PRODUCT}-${PRODUCT_VERSION}/crowd-webapp/WEB-INF/classes/crowd-init.properties
RUN cd ${PRODUCT}-${PRODUCT_VERSION} && sed -i -e 's#start "$@"#run "$@"#' apache-tomcat/bin/startup.sh

EXPOSE 8095
VOLUME /opt/${PRODUCT}/

CMD /home/${PRODUCT}/${PRODUCT}-${PRODUCT_VERSION}/start_crowd.sh
