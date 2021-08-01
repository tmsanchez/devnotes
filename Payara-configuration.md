# Payara 5.2020.5 Jaybird Configuration

Go to _bin_ folder where *Payara* is installed

```
cd payaraInstallationPath/bin
```

## Basic commands

### Start Payara Server

```
asadmin start-domain
```

### Start domain

```
asadmin start-domain
```

## FIREBIRDSQL Driver Configuration

1. Stop payara server 
2. Copy jaybird-3.09.jar to payara-5.2020.5/glassfish/domains/domain1/lib

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

3. Start payara server

## JDBC Connection Pool Configuration

1. Open _Payara_ console

```
http://localhost:4848
```

2. Go to *Resources / JDBC / JDBC Connection Pools*
3. Clik on *New* button

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_1.png)
...

### Connection Pool settings

In *General Settings* fill following values and then click  *Next* button

| Field                   | Sample Value             |
|-------------------------|--------------------------|
| Pool Name               | MyDbPool                 |
| Resource Type           | java.sql.DataSource      |
| DataBase Driver Vendor  | Firebird Jaybird         |
| Introspect              | unchecked                |

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/master/jdbc_config_2.png)
...

In _Step 2 of 2_ complete following information in *General Settings*

| Field                   | Sample Value                           |
|-------------------------|----------------------------------------|
| DataSource Classname    | org.firebirdsql.ds.FBSimpleDataSource  |

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_3.png)
...

Complete following data in *Additial Properties*

| Name        | Value                           |
|-------------|---------------------------------|
| password    | thepassword                     |
| userName    | USERNAMEVALUE                   |
| database    | //localhost/databasename        |

value for *database* **must not include** *jdbc* prefix

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_config_4.png)
...

### JDBC Resource settings

1. Go to *Resources / JDBC / JDBC Resources*
2. Clic on *New* button

...
![Payra console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_resource_1.png)
...

3. In *New JDBC Resource* form fill following values and click on *OK* button

| Field        | Value                                  |
|--------------|----------------------------------------|
| JNDI Name    | jdbc/ResourceName                      |
| Pool Name    | Seleccionar el Pool creado previamente |
| Descripction | Texto descriptivo del recurso JDBC     |

...
![Payara console](https://github.com/tmsanchez/devnotes/blob/main/jdbc_resource_2.png)
...

## Done

JDBC Resource is ready to use in your Java application