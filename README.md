## franquigimmvn
Proyecto de muestra JSF JPA con Java y mvn

Para descargar el projecto desde github hacer, abrir un terminal y en un directorio cualquiera:

```
git clone https://github.com/yzeballos/franquigimmvn.git franquigimmvn
```

Crear el siguiente esquema en una base de datos MySql:
```
CREATE DATABASE `franquigimsch` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ /*!80016 DEFAULT ENCRYPTION='N' */;
```

Crear las siguientes tablas:

```
CREATE TABLE `franquigimsch`.`sucursal` (
  `id` int NOT NULL AUTO_INCREMENT,
  `nombre` varchar(100) DEFAULT NULL,  
  `airelibre` tinyint(1) DEFAULT NULL,
  `longitud` float(10,5) NOT NULL,
  `latitud` float(10,5) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


CREATE TABLE `franquigimsch`.`afiliado` (
  `id` int NOT NULL AUTO_INCREMENT,
  `nombre` varchar(100) DEFAULT NULL,  
  `plan` varchar(1) DEFAULT NULL,
  `descuento` float(10,5) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
Y se recomiendan los siguientes datos de prueba:

```
INSERT INTO `franquigimsch`.`sucursal` (`id`, `nombre`, `airelibre`, `longitud`, `latitud`) VALUES ('1', 'Sucursal1', '1', ' 	-56.188', ' 	-34.333');
INSERT INTO `franquigimsch`.`sucursal` (`id`, `nombre`, `airelibre`, `longitud`, `latitud`) VALUES ('2', 'SucursalCordon', '0', ' 	-56.18472', '-34.90925');
INSERT INTO `franquigimsch`.`sucursal` (`id`, `nombre`, `airelibre`, `longitud`, `latitud`) VALUES ('3', 'SucursalPalermo', '1', ' 	-56.178', ' 	-34.907');

INSERT INTO `franquigimsch`.`afiliado` (`id`, `nombre`, `plan`, `descuento`) VALUES ('1', 'Juancito', 'B', '50');
INSERT INTO `franquigimsch`.`afiliado` (`id`, `nombre`, `plan`, `descuento`) VALUES ('2', 'Tafarel', 'C', '10');
```
El servidor de base de datos MySql se asume en el puerto estandar (3306).

Importante: En "./franquigim/src/conf/persist.xml" Se pueden cambiar las credenciales de MySql de javax.persistence.jdbc.user y javax.persistence.jdbc.password, que en este ejemplo tienen el valor de "root".

```
      <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/franquigimsch?useSSL=false"/>
      <property name="javax.persistence.jdbc.user" value="root"/>
      <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
      <property name="javax.persistence.jdbc.password" value="root"/>
```      

## Configuracion
El directorio de glassfish requiere tener un archivo ".env" (sic) con la API_KEY de clima y eventualmente todas las API_KEY que se quieran mantener privadas.
Asi que si el directorio de glassfish es:
```      
/home/misay/servers/glassfish-5.0.1/glassfish5
```      
Ahi se debe crear el archivo .env

```      
touch ".env"
ls
drwxr-xr-x  2 misay misay 4,0K ene 15  2019 bin
-rw-rw-r--  1 misay misay   47 abr 20 17:42 .env
drwxr-xr-x 11 misay misay 4,0K ene 15  2019 glassfish
drwxr-xr-x  4 misay misay 4,0K ene 15  2019 javadb
drwxr-xr-x  6 misay misay 4,0K ene 15  2019 mq
```      

y agregarle el contenido:
```      
API_KEY_CLIMA=312321321321312
```      
Donde 312321321321312 es un valor valido.

Tambien se debe cambiar en el el .pom el directorio del glassfish para que funcione el deploy del plugin de artifactId maven-glassfish-plugin.

```      
             <plugin>
                <groupId>org.glassfish.maven.plugin</groupId>
                <artifactId>maven-glassfish-plugin</artifactId>
                <version>2.1</version>
                <configuration>
                    <glassfishDirectory>/home/misay/servers/glassfish-5.0.1/glassfish5/glassfish</glassfishDirectory>
                    <user>admin</user>
                    <passwordFile>/home/misay/servers/glassfish-5.0.1/glassfish5/glassfish/domains/domain1/config/domain-passwords</passwordFile>
                    <domain>
                        <name>domain1</name>
                        <httpPort>8080</httpPort>
                        <adminPort>4848</adminPort>
                    </domain>
                    <components>
                        <component>
                            <name>${project.artifactId}</name>
                            <artifact>target/${project.artifactId}-${project.version}.war</artifact>
                        </component>
                    </components>
                    <debug>true</debug>
                    <terse>false</terse>
                    <echo>true</echo>
                </configuration>
            </plugin>
```      
Es decir en este ejemplo son:
```      
<glassfishDirectory>/home/misay/servers/glassfish-5.0.1/glassfish5/glassfish</glassfishDirectory>
 <passwordFile>/home/misay/servers/glassfish-5.0.1/glassfish5/glassfish/domains/domain1/config/domain-passwords</passwordFile>
```
Se deben sustituir por los valores correspondientes del glassfish local.

## Compilacion y ejecucion

Comenzar el glassfish con normalidad.
Tambien se puede iniciar con el siguiente tip:
``` 
~/servers/glassfish-5.0.1/glassfish5$ sudo java -Djava.endorsed.dirs=$PWD/glassfish/modules/endorsed -jar glassfish/modules/glassfish.jar
``` 
luego se puede hacer todo con "mvn"

``` 
$ mvn clean install
$ mvn glassfish:deploy
``` 

