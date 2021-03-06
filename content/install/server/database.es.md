+++
date = "2017-04-15T14:39:04+02:00"
title = "Configuraciones de base de datos"
url = "es/database-settings"

[menu.install]
  identifier = "database-settings-es"
  parent = "install_server"
  weight = 1
+++

Esta guía provee instrucciones para usar motores de base de datos. Por favor nota que esto es opcional. El motor de almacenaje por defecto es una base de datos SQLite embebida que no requiere instalarse o configurarse.

# Configurar MySQL

El siguiente ejemplo demuestra la configuración de una base de datos MySQL. Revisa la [documentación del controlador oficial](https://github.com/go-sql-driver/mysql#dsn-data-source-name) para encontrar opciones de configuración y otros ejemplos.

```diff
version: '2'

services:
  drone-server:
    image: drone/drone:{{% version %}}
    environment:
+     DRONE_DATABASE_DRIVER: mysql
+     DRONE_DATABASE_DATASOURCE: root:password@tcp(1.2.3.4:3306)/drone?parseTime=true
```

# Configurar Postgres

El siguiente ejemplo muestra la configuración de una base de datos Postgres. Revisa la [documentación del controlador oficial](https://www.postgresql.org/docs/current/static/libpq-connect.html#LIBPQ-CONNSTRING) para encontrar opciones de configuración y otros ejemplos.

```diff
version: '2'

services:
  drone-server:
    image: drone/drone:{{% version %}}
    environment:
+     DRONE_DATABASE_DRIVER: postgres
+     DRONE_DATABASE_DATASOURCE: postgres://root:password@1.2.3.4:5432/postgres?sslmode=disable
```

# Creación de la base de datos

Drone no crea la base de datos automáticamente. Si estas usando el controlador de MySQL o Postgres es necesario crear la base de datos usando el comando `CREATE DATABASE`

# Migración de la base de datos

Drone maneja la migración de la base de datos automáticamente, incluyendo la creación inicial de tablas e índices. Nuevas versiones de Drone actualizarán la base de datos a menos que se indique en las notas de lanzamiento.

# Respaldos de la base de datos

Drone no realiza respaldos de la base de datos. Esto debería se manejado por herramientas externas proveídas por el vendedor de base de datos elegido.

# Archivando la base de datos

Drone no archiva datos; se considera fuera del alcance del proyecto. Drone es algo conservador con la cantidad de datos que guarda, sin embargo, deberías asumir que los logs de la base de datos incrementen el tamaño de tu base de datos considerablemente.
