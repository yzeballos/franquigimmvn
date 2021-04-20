## franquigim
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
