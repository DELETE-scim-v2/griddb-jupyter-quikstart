# Introduction

This projects lets you test [https.//griddb.net](griddb) with python in a jupyter notebook.

# Prerequisites

- docker (https://www.docker.com/)
- docker-compose (https://docs.docker.com/compose/)

# Setup / Installation

Run `docker-compose build`

# Usage

Run `docker-compose up -d`

To get the URL for jupyter, run: `docker-compose logs jupyter` (copy the 127.0.0.1:8888/?token=XXXXXXX url)

# Example script in python

```python3
import pandas as pd
import jaydebeapi

conn = jaydebeapi.connect("com.toshiba.mwcloud.gs.sql.Driver",
                           "jdbc:gs://griddb:20001/defaultCluster/public?notificationMember:127.0.0.1:20001",
                           ["admin", "admin"],
                          "/usr/share/java/gridstore-jdbc-4.5.0.jar",)

curs = conn.cursor()
curs.execute('CREATE TABLE Sensor1(datetime TIMESTAMP PRIMARY KEY, payload FLOAT)')
curs.execute("INSERT into Sensor1 values (now(), 45.6)")
curs.execute("SELECT * FROM Sensor1")
curs.fetchall()
curs.close()

sql = ("SELECT * FROM Sensor1")
sql_query = pd.read_sql_query(sql, conn)
sql_query
```