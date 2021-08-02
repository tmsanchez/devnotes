# Configuracion de FirebirdSql en Payara 5.2020.5

Para configurar *Payara* es necesario ingresar a la carpeta _bin_ donde está instalado el servidor

```
cd pathDondeEstaPayara/bin
```

## Comandos útiles

## Iniciar el Servidor

```
asadmin start-domain
```

## Detener el Servidor

```
asadmin start-domain
```

## Configuración del Driver de FIREBIRD

1. Detener el servidor 
2. Copiar el archivo jaybird-3.09.jar a la carpeta payara-5.2020.5/glassfish/domains/domain1/lib

```
$cd /home/users/myuser/java/payara-5.2020.5/glassfish/domains/domain1/lib
$ ll
total 1136
drwxr-xr-x 1 usuario 197121       0 oct.  9 10:05 applibs/
drwxr-xr-x 1 usuario 197121       0 oct.  9 10:05 classes/
drwxr-xr-x 1 usuario 197121       0 oct. 15 21:37 databases/
drwxr-xr-x 1 usuario 197121       0 oct. 15 21:37 ext/
-rw-r--r-- 1 usuario 197121 1159782 may. 22 14:36 jaybird-3.0.9.jar
```

3. Iniciar el servidor

## Configuración del JDBC Connection Pool

1. Ingresar al navegador a la siguiente dirección

```
http://localhost:4848
```

2. Seleccionar *Resources / JDBC / JDBC Connection Pools*
3. Dar clic en el botón *New*

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_1.png)
...

### Información para el Connection Pool

En el apartado *General Settings* llenar los siguientes valores y presionar el botón *Next*

| Field                   | Sample Value             |
|-------------------------|--------------------------|
| Pool Name               | MyDbPool                 |
| Resource Type           | java.sql.DataSource      |
| DataBase Driver Vendor  | Firebird Jaybird         |
| Introspect              | unchecked                |

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_2.png)
...

En el paso 2 de 2 llenar la siguiente información en *General Settings*

| Field                   | Sample Value                           |
|-------------------------|----------------------------------------|
| DataSource Classname    | org.firebirdsql.ds.FBSimpleDataSource  |

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_3.png)
...

Capturar la siguiente información en *Additial Properties*

| Name        | Value                           |
|-------------|---------------------------------|
| password    | thepassword                     |
| userName    | USERNAMEVALUE                   |
| database    | //localhost/databasename        |

el valor de *database* no debe llevar el prefijo *jdbc*

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_4.png)
...

### Información para el JDBC Resource

1. Seleccionar *Resources / JDBC / JDBC Resources*
2. Dar clic en el botón *New*

...
![Payra console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_resource_1.png)
...

3. En la pantalla *New JDBC Resource* completar la siguiente información y presionar en el botón *OK*

| Field        | Value                                  |
|--------------|----------------------------------------|
| JNDI Name    | jdbc/ResourceName                      |
| Pool Name    | Seleccionar el Pool creado previamente |
| Descripction | Texto descriptivo del recurso JDBC     |

...
![Payra console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_resource_2.png)
...

## Listo

El recurso JDBC Resource está listo para ser utilizado en la aplicación Java
