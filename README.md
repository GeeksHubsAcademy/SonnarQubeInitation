# SonnarQubeInitation
Repository for install and run sonnar-runner

## Prerrequesitos.
Debemos tener instalado Java, para ello podemos descargar OpenJDK [página](https://openjdk.java.net/install/).
O podemos instalar OracleJDK desde su [página](https://www.oracle.com/java/technologies/javase-jdk8-downloads.html)

## Instalación.
Debemos descargar el runner para el sistema operativo en el que vamos a trabajar. Desde la página de [sonarqube](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)

**Si instalamos sobre linux seguiremos los siguientes puntos:**

Crearemos un directorio donde descargar el runner
```
$ sudo mkdir /opt/sonarscanner
```
Nos cambiamos a dicho directorio. 
```
$ cd /opt/sonarscanner
``` 
Y procedemos a bajar el repo.
```
$ sudo wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.2.0.1227-linux.zip
```
Descomprimimos el proyecto
```
$ sudo unzip sonar-scanner-cli-3.2.0.1227-linux.zip
```
Eliminamos el zip
```
$ sudo rm sonar-scanner-cli-3.2.0.1227-linux.zip
```
Posteriormente modificaremos el archivo de configuración de sonar para añadir y apuntar hacia el servidor donde tenemos instalado SonarQube
```
$ sudo nano sonar-scanner-3.2.0.1227-linux/conf/sonar-scanner.properties
```
Buscaremos las siguientes líneas las descomentaremos y añadiremos los siguientes datos:
```
sonar.host.url=[url de nuestro server]
```
A continuación cambairamos los permisos para que se pueda ejecutar.
```
$ sudo chmod +x sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner
```
Y por último crearemos un link simbólico para poder ejecutar el mismo en cualquier directorio de nuestro sistema operativo.
```
$ sudo ln -s /opt/sonarscanner/sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner
``` 
**Si instalamos sobre windows seguiremos los siguientes puntos:**

 Descargamos el instalador en una carpeta y lo ejecutamos.
 Una vez ejecutado debemos buscar el archivo de configuración de sonnarqube en el directorio de instalación que hemos marcado.
 Descomnetamos la línea y añadimos la url de la máquina.
```
 sonar.host.url=[url de nuestro server]
```
## Uso.

Para poder utilizar el cliente en nuestro proyecto, debemos seguir los siguientes pasos.
En el proyecto debemos crear un archivo properties.
```
$ nano sonar-project.properties
```

Añadiremos las siguientes líneas, sustituyendo las líneas que nos intersa.
```
 must be unique in a given SonarQube instance
sonar.projectKey=my:project

# --- optional properties ---

# defaults to project key
#sonar.projectName=My project
# defaults to 'not provided'
#sonar.projectVersion=1.0
 
# Path is relative to the sonar-project.properties file. Defaults to .
#sonar.sources=.
 
# Encoding of the source code. Default is default system encoding
#sonar.sourceEncoding=UTF-8
  
```
Una vez lo tenemos sólo debemos ejecutar.
```
$ sonar-scanner
```
Si hemos activado la seguridad por Token debemo indicarlo.
```
$ sonar-scanner -D sonar.login=your_token_here
```
