FROM centos:latest

RUN yum update -y
RUN yum install -y \
  curl \
  java \
  java-1.8.0-openjdk-devel \
  git \
  vim \
  unzip

COPY wildfly-11.0.0.Final.zip /opt
WORKDIR /opt
RUN unzip wildfly-11.0.0.Final.zip
RUN ln -s wildfly-11.0.0.Final wildfly
RUN cp /opt/wildfly/standalone/configuration/standalone.xml{,.bak}
RUN sed -i 's!<inet-address value="${jboss.bind.address.management:127.0.0.1}"/>!<any-address/>!' /opt/wildfly/standalone/configuration/standalone.xml
RUN sed -i 's!<inet-address value="${jboss.bind.address:127.0.0.1}"/>!<any-address/>!' /opt/wildfly/standalone/configuration/standalone.xml

COPY myapp.war /tmp
COPY postgresql-42.1.1.jar /tmp
COPY jboss-cli.txt /tmp
COPY script.sh /opt

WORKDIR /opt/wildfly
RUN touch /tmp/foo_002.txt

CMD /opt/script.sh
