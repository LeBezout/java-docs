# In-Memory / Java Databases Overview

## Main librairies

* [Apache Derby](http://db.apache.org/derby/) - [Getting started](https://builds.apache.org/job/Derby-docs/lastSuccessfulBuild/artifact/trunk/out/getstart/index.html)
* [Hyper SQL DB](http://hsqldb.org/) - [Getting started](http://hsqldb.org/doc/2.0/guide/index.html)
* [H2 Database Engine](http://www.h2database.com/) - [Getting started](http://www.h2database.com/html/quickstart.html) - [Cheat Sheet](http://www.h2database.com/html/cheatSheet.html)

## Maven Dependencies

### Apache Derby

```xml
<dependency>
  <groupId>org.apache.derby</groupId>
  <artifactId>derby</artifactId>
  <version>10.14.1.0</version>
  <scope>test</scope>
</dependency>
```

### Hyper SQL

```xml
<dependency>
  <groupId>org.hsqldb</groupId>
  <artifactId>hsqldb</artifactId>
  <version>2.4.0</version>
  <scope>test</scope>
</dependency>
```

### H2

```xml
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <version>1.4.196</version>
  <scope>test</scope>
</dependency>
```

## Overview

| Item              | Apache Derby | Hyper SQL DB | H2 Database Engine |
|-------------------|--------------|--------------|--------------------|
| Driver Class name | `org.apache.derby.jdbc.EmbeddedDriver` | `org.hsqldb.jdbc.JDBCDriver` | `org.h2.Driver` |
| Hibernate Dialect | `org.hibernate.dialect.DerbyDialect` | `org.hibernate.dialect.HSQLDialect` | `org.hibernate.dialect.H2Dialect` |
| Create file database | `jdbc:derby:target/junit/db/my_db;create=true` | `jdbc:hsqldb:file:target/junit/db/my_db;create=true` | `jdbc:h2:file:target/junit/db/my_db` |
| Create memory database | `jdbc:derby:memory:my_db;create=true` | `jdbc:hsqldb:mem:my_db` | `jdbc:hsqldb:mem:my_db` | `jdbc:h2:mem:my_db` |
| Shutdown database | `jdbc:derby:target/junit/db/my_db;shutdown=true` |  `jdbc:hsqldb:file:target/junit/db/my_db;shutdown=true` | database is closed when the last connection to it is closed |

## Drivers

| Librairy | Driver Class name |
|----------|-------------------|
| **Apache Derby** | `org.apache.derby.jdbc.EmbeddedDriver` |
| **Hyper SQL DB** | `org.hsqldb.jdbc.JDBCDriver` |
| **H2 Database Engine** | `org.h2.Driver` |

## Hibernate Dialect

| Librairy | Dialect Class name |
|----------|--------------------|
| **Apache Derby** | `org.hibernate.dialect.DerbyDialect` |
| **Hyper SQL DB** | `org.hibernate.dialect.HSQLDialect` |
| **H2 Database Engine** | `org.hibernate.dialect.H2Dialect` |

## Create database

### File

| Librairy | JDBC String | User | Password |
|----------|-------------|------|----------|
| **Apache Derby** | `jdbc:derby:target/junit/db/my_db;create=true` | :no_entry_sign: | :no_entry_sign: |
| **Hyper SQL DB** | `jdbc:hsqldb:file:target/junit/db/my_db;create=true` | `SA` | :no_entry_sign: |
| **H2 Database Engine** | `jdbc:h2:file:target/junit/db/my_db` | `sa` | :no_entry_sign: |

### In-Memory

| Librairy | JDBC String | User | Password |
|----------|-------------|------|----------|
| **Apache Derby** | `jdbc:derby:memory:my_db;create=true` | :no_entry_sign: | :no_entry_sign: |
| **Hyper SQL DB** | `jdbc:hsqldb:mem:my_db` | `SA` | :no_entry_sign: |
| **H2 Database Engine** | `jdbc:h2:mem:my_db` | `sa` | :no_entry_sign: |

## Shutdown database

| Librairy | JDBC String | User | Password |
|----------|-------------|------|----------|
| **Apache Derby** | `jdbc:derby:target/junit/db/my_db;shutdown=true` | :no_entry_sign: | :no_entry_sign: |
| **Hyper SQL DB** | `jdbc:hsqldb:file:target/junit/db/my_db;shutdown=true` | `SA` | :no_entry_sign: |
| **H2 Database Engine** | database is closed when the last connection to it is closed | :no_entry_sign: | :no_entry_sign: |

## Compatibility Modes

| DBMS Provider | Apache Derby | Hyper SQL DB | H2 Database Engine |
|-------------|--------------|--------------|--------------------|
| Oracle | :no_entry_sign: | `sql.syntax_ora=true` | `MODE=Oracle` |
| MySQL | :no_entry_sign: | `sql.syntax_mys=true` | `MODE=MySQL` |
| PostgreSQL | :no_entry_sign: | `sql.syntax_pgs=true` | `MODE=PostgreSQL` |
| DB2 | :no_entry_sign: | `sql.syntax_db2=true` | `MODE=DB2` |
| MS SQLServer | :no_entry_sign: | `sql.syntax_mss=true` | `MODE=MSSQLServer` |
| Derby | :no_entry: | :no_entry_sign: | `MODE=Derby` |
| HSQLDB | :no_entry_sign: | :no_entry: | `MODE=HSQLDB` |
| H2 | :no_entry_sign: | :no_entry_sign: |  :no_entry: |

* [H2 Compatibility page](http://www.h2database.com/html/features.html#compatibility)
* [HSQLDB Compatibility page](http://hsqldb.org/doc/guide/compatibility-chapt.html)

## Remarks

### Apache Derby

> To remove an in-memory database, use the connection URL attribute drop as follows: `jdbc:derby:memory:my_db;drop=true`

> When you drop the database, Derby issues what appears to be an error but is actually an indication of success. You need to catch error 08006, as described in "The WwdEmbedded program" in Getting Started with Derby.

### Hyper SQL

> If no username or password is specified, the default SA user and an empty password are used

> Both the username and password are case-sensitive. (The exception is the default SA user, which is not case-sensitive). If no username or password is specified, the default SA user and an empty password are used.

> A connection property `ifexists=true` allow connection to an existing database only and avoid creating a new database.

### H2

> By default, a new database is automatically created if it does not exist yet.

> `;DB_CLOSE_DELAY=<seconds>` The parameter `<seconds>` specifies the number of seconds to keep a database open after the last connection to it was closed.

> [Database URL Overvieww](http://www.h2database.com/html/features.html#database_url)
