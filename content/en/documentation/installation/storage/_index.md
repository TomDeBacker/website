---
title: "Storage"
subtitle: "JobRunr supports both SQL and NoSQL databases"
date: 2020-04-30T11:12:23+02:00
layout: "documentation"
menu: 
  main: 
    identifier: storage
    parent: 'installation'
    weight: 5
---
JobRunr stores the job details for each job using a `StorageProvider` and supports all major SQL databases and NoSQL databases.

> __Important__: you will need to add the correct dependency (jdbc-driver) for each of the databases below.

## SQL databases
By default, JobRunr will automatically create the necessary tables for your database. If however you do not want to give the JobRunr DataSource DDL rights, you can easily create the tables JobRunr uses yourself using one of the following methods:


> Running MySQL or MariaDB? Make sure [your connection string]() is setup that it [UTC timestamps correctly](https://stackoverflow.com/questions/1646171/mysql-datetime-fields-and-daylight-savings-time-how-do-i-reference-the-extra).


#### Run the DatabaseCreator
The DatabaseCreator class allows you to create the necessary tables using a terminal. You must provide a user that has DDL rights.

```
java -cp jobrunr-${jobrunr.version}.jar org.jobrunr.storage.sql.common.DatabaseCreator {jdbcUrl} {userName} {password}
```

If the command succeeds, a confirmation message will be shown.

#### Apply the SQL scripts yourself
- __Oracle__ -  apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/common/migrations) overriding most of these sql scripts with the Oracle specific scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/oracle/migrations).
- __Postgres__ - apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/common/migrations).
- __MySql__ - apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/common/migrations) overriding some of these sql scripts with the MySql specific scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/mariadb/migrations).
- __MsSqlServer__ - apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/common/migrations) overriding some of these sql scripts with the MsSqlServer specific scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/sqlserver/migrations).
- __Postgres__ - apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/common/migrations).
- __DB2__ - apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/db2/migrations).
- __MariaDB__ - apply all the sql scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/common/migrations) overriding some of these sql scripts with the MariaDB specific scripts found [here](https://github.com/jobrunr/jobrunr/tree/master/core/src/main/resources/org/jobrunr/storage/sql/mariadb/migrations).

Once you created the tables, you can configure JobRunr as follows (when using `jobrunr-spring-boot-starter`, this is not necessary):

```java
JobRunr.configure()
    .useStorageProvider(new DefaultSqlStorageProvider(dataSource, DatabaseOptions.SKIP_CREATE))
    .useBackgroundJobServer()
    .initialize();
```

### TablePrefix
JobRunr also supports a table prefix which will prefix all tables with a custom prefix. This comes in handy if you want to specify a schema for your tables.


## NoSQL databases
- __ElasticSearch__ - JobRunr will create the necessary indices to save all Jobs and Recurring Jobs automatically for you. They will be prefixed with `jobrunr_`
  - use the `ElasticSearchStorageProvider` together with a `RestHighLevelClient`
- __Mongo__ - JobRunr will create a database called `jobrunr` and all the necessary collection to save all Jobs and Recurring Jobs automatically for you
  - use the `MongoDBStorageProvider` - JobRunr supports all Mongo versions from Mongo 3.4 and up.
- __Amazon DocumentDB__ - JobRunr will create a database called `jobrunr` and all the necessary collection to save all Jobs and Recurring Jobs automatically for you
  - use the `AmazonDocumentDBStorageProvider`
- __Redis__ - JobRunr will create all necessary datatypes (Strings, Sets, Hashes, ... ) automatically for you. You can choose out of two implementations: 
  - either the `JedisRedisStorageProvider` which uses Jedis.
  - and the `LettuceRedisStorageProvider` which uses Lettuce. If you use this `StorageProvider` you also need to add a dependency to `org.apache.commons:commons-dbcp2` as the Lettuce driver is not thread-safe when using Redis Transactions.
- __InMemory__ - JobRunr comes with an InMemoryStorageProvider, which is ideal for lightweight tasks that are server-instance specific and where persistence is not important. Note that if you use the `InMemoryStorageProvider`, you can not scale horizontally as the storage is not shared.
  - use the `InMemoryStorageProvider` for in-memory support
