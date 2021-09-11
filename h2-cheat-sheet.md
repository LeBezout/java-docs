# H2 Cheat Sheet

## Documentation Links

* [H2 Database Engine - main site](http://www.h2database.com/html/main.html)
* [H2 Database Engine Cheat Sheet](http://www.h2database.com/html/cheatSheet.html)
* [Data Types](http://www.h2database.com/html/datatypes.html)
* [Database URL Overview](http://www.h2database.com/html/features.html#database_url)

## Summury

* JDBC Driver class name : `org.h2.Driver`
* Hibernate Dialect class name : `org.hibernate.dialect.H2Dialect`
* JDBC URL (File) : `jdbc:h2:file:./target/junit/db/my_db`
* JDBC URL (Memory) : `jdbc:h2:mem:my_db`
* Validation Query : `select 1`

## Maven

```xml
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <version>1.4.200</version>
  <scope>test</scope>
</dependency>
```

:link: <https://search.maven.org/artifact/com.h2database/h2/>

## Web Console

### Launch from CLI

Sample shell :

```bash
#!/bin/bash
readonly CLASSPATH="/opt/liquibase/lib/h2-1.4.200.jar"
echo "Launching H2 console..."
java -cp "${CLASSPATH}" org.h2.tools.Console
```

### Integrate in Webapp

:bulb: <http://www.h2database.com/html/tutorial.html#usingH2ConsoleServlet>

`web.xml` snippet :

```xml
    <servlet>
        <servlet-name>H2Console</servlet-name>
        <servlet-class>org.h2.server.web.WebServlet</servlet-class>
        <!--
        <init-param>
            <param-name>webAllowOthers</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>trace</param-name>
            <param-value></param-value>
        </init-param>
        -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>H2Console</servlet-name>
        <url-pattern>/admin/h2/*</url-pattern>
    </servlet-mapping>
```

## CLI

### Execute SQL

:bulb: <http://www.h2database.com/javadoc/org/h2/tools/Shell.html>

Sample shell :

```bash
#!/bin/bash
readonly DB_PATH="./H2/DEMO_DB"
readonly MODE="MySQL"
readonly USER="sa"
readonly CLASSPATH="/opt/liquibase/lib/h2-1.4.200.jar"
if [ $# = 0 ]; then
  java -cp "${CLASSPATH}" org.h2.tools.Shell -help
else
  echo "Executing SQL against H2 ..."
  java -cp "${CLASSPATH}" org.h2.tools.Shell -sql "$1" -url "jdbc:h2:file:${DB_PATH};MODE=${MODE}" -user "${USER}"
fi
```

## Troubleshooting

### IllegalStateException: Unable to read the page at position

A driver version is used for creation and another for read.

### NUMBER(*, 0)

Not supported! Replace with `number(10, 0)`, `number(38, 0)`,  ...

### Deffered FK

Not supported!
