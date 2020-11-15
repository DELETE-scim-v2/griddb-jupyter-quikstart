FROM jupyter/scipy-notebook

USER root

RUN apt update && apt install default-jre telnet -y

RUN wget https://repo1.maven.org/maven2/com/github/griddb/gridstore-jdbc/4.5.0/gridstore-jdbc-4.5.0.jar && \
    mv gridstore-jdbc-4.5.0.jar /usr/share/java/

RUN chown 777 /usr/share/java/gridstore-jdbc-4.5.0.jar

USER $NB_UID

RUN pip install jaydebeapi