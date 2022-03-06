# Proyecto de prueba de Backend con Maven y wildfly



## Standalone configuración

Agregar la siguiente configuracion al wildfly  
En seguridad cambiar por los credenciales de postgres

    <subsystem xmlns="urn:jboss:domain:datasources:5.0">  
        <datasources>
            <datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS" enabled="true" use-java-context="true" statistics-enabled="${wildfly.datasources.statistics-enabled:${wildfly.statistics-enabled:false}}">
                <connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE</connection-url>
                <driver>h2</driver>
                <security>
                    <user-name>sa</user-name>
                    <password>sa</password>
                </security>
            </datasource>
            <datasource jndi-name="java:jboss/datasources/laboratorio" pool-name="LaboratorioPostgres" enabled="true" use-java-context="true">
                <connection-url>jdbc:postgresql://localhost:5432/backend</connection-url>
                <driver>postgres</driver>
                <pool>
                    <max-pool-size>20</max-pool-size>
                </pool>
                <security>
                    <user-name>postgres</user-name>
                    <password>admin</password>
                </security>
            </datasource>
            <drivers>
                <driver name="h2" module="com.h2database.h2">
                    <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
                </driver>
                <driver name="postgres" module="org.postgresql.driver">
                    <driver-class>org.postgresql.Driver</driver-class>
                    <xa-datasource-class>org.postgresql.xa.PGXADataSource</xa-datasource-class>
                </driver>
            </drivers>
        </datasources>
    </subsystem>


## Configuracion de persistencia

Crear una base de datos en postgres denominada ` backend `  
Ejecutar el script denomidado ``SCRIPT.sql`` en la base de datos creada