# In-Memory Java Databases Overview

## Main librairies

 ![Logo Derby](https://db.apache.org/derby/docs/10.0/images/derby-logo-web.png)  ![Logo HSQL](http://hsqldb.org/images/hypersql_logo.png)  ![Logo H2](http://www.h2database.com/html/images/h2-logo-2.png)

* [Apache Derby](http://db.apache.org/derby/) - [Getting started](https://db.apache.org/derby/papers/DerbyTut/index.html)
* [Hyper SQL DB](http://hsqldb.org/) - [Getting started](http://hsqldb.org/doc/2.0/guide/index.html)
* [H2 Database Engine](http://www.h2database.com/) - [Getting started](http://www.h2database.com/html/quickstart.html) - [Cheat Sheet](http://www.h2database.com/html/cheatSheet.html)

## Configuration

### Maven Dependencies

#### Apache Derby

```xml
<dependency>
  <groupId>org.apache.derby</groupId>
  <artifactId>derby</artifactId>
   <version>10.15.2.0</version>
  <scope>test</scope>
</dependency>
```

:link: <https://search.maven.org/artifact/org.apache.derby/derby/10.15.2.0/jar>

#### Hyper SQL

```xml
<dependency>
  <groupId>org.hsqldb</groupId>
  <artifactId>hsqldb</artifactId>
  <version>2.5.1</version>
  <scope>test</scope>
</dependency>
```

:link: <https://search.maven.org/artifact/org.hsqldb/hsqldb/2.5.1/jar>

#### H2

```xml
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <version>1.4.200</version>
  <scope>test</scope>
</dependency>
```

:link: <https://search.maven.org/artifact/com.h2database/h2/1.4.200/jar>

### Drivers

| Librairy | Driver Class name |
|----------|-------------------|
| **Apache Derby** | `org.apache.derby.jdbc.EmbeddedDriver` |
| **Hyper SQL DB** | `org.hsqldb.jdbc.JDBCDriver` |
| **H2 Database Engine** | `org.h2.Driver` |

### Hibernate Dialect

| Librairy | Dialect Class name |
|----------|--------------------|
| **Apache Derby** | `org.hibernate.dialect.DerbyDialect` |
| **Hyper SQL DB** | `org.hibernate.dialect.HSQLDialect` |
| **H2 Database Engine** | `org.hibernate.dialect.H2Dialect` |

### Create database

#### File

| Librairy | JDBC String | User | Password |
|----------|-------------|------|----------|
| **Apache Derby** | `jdbc:derby:target/junit/db/my_db;create=true` | :no_entry_sign: | :no_entry_sign: |
| **Hyper SQL DB** | `jdbc:hsqldb:file:./target/junit/db/my_db;create=true` | `SA` | :no_entry_sign: |
| **H2 Database Engine** | `jdbc:h2:file:./target/junit/db/my_db` | `sa` | :no_entry_sign: |

#### In-Memory

| Librairy | JDBC String | User | Password |
|----------|-------------|------|----------|
| **Apache Derby** | `jdbc:derby:memory:my_db;create=true` | :no_entry_sign: | :no_entry_sign: |
| **Hyper SQL DB** | `jdbc:hsqldb:mem:my_db` | `SA` | :no_entry_sign: |
| **H2 Database Engine** | `jdbc:h2:mem:my_db` | `sa` | :no_entry_sign: |

### Shutdown database

| Librairy | JDBC String | User | Password |
|----------|-------------|------|----------|
| **Apache Derby** | `jdbc:derby:target/junit/db/my_db;shutdown=true` | :no_entry_sign: | :no_entry_sign: |
| **Hyper SQL DB** | `jdbc:hsqldb:file:target/junit/db/my_db;shutdown=true` | `SA` | :no_entry_sign: |
| **H2 Database Engine** | database is closed when the last connection to it is closed | :no_entry_sign: | :no_entry_sign: |

### Validation Queries

| Librairy | Validation Query |
|----------|--------------------|
| **Apache Derby** | `values 1` |
| **Hyper SQL DB** | `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS` |
| **H2 Database Engine** | `select 1` |

:link: <http://vondrnotes.blogspot.com/2012/05/validationquery-for-different-databases.html>

### Compatibility Modes

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

* :link: [H2 Compatibility page](http://www.h2database.com/html/features.html#compatibility)
* :link: [HSQLDB Compatibility page](http://hsqldb.org/doc/guide/compatibility-chapt.html)


### Liquibase Type Name

| Librairy | Type Name |
|----------|-----------|
| **Apache Derby** | `derby` |
| **Hyper SQL DB** | `hsqldb` |
| **H2 Database Engine** | `h2` |

:link: <https://www.liquibase.org/databases.html>

## Data Types

* :link: [Derby 10.15 Data Types](https://db.apache.org/derby/docs/10.15/ref/crefsqlj31068.html)
* :link: [HSQLDB Data Types](http://www.hsqldb.org/doc/guide/sqlgeneral-chapt.html#sgc_types_ops)
* :link: [H2 Data Types](http://www.h2database.com/html/datatypes.html)

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

> :link: [Database URL Overview](http://www.h2database.com/html/features.html#database_url)
