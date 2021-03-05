##### DANIEL DIAZ-DELGADO


En esta actividad hemos instalado las aplicación :
	-Java.
	-Apache.
	-Tomcat.
	-openSSh.
Para ellos nos hemos ayudado de estos comandos.
En la instalación de los mismo usamos :
-**sudo apt-get install default-jdk** para instalar Java
**-sudo apt install apache2** para inatalar Apache
Para instalar TOMCAT añadimos un usuario con el comando **sudo useradd –m –U –d /opt/tomcat –s /bin/false tomcat**

Nos vamos a la carpeta cd temp y ejecutamos el codigo **wget http://apache.rediris.es/tomcat/tomcat-9/v9.0.43/bin/apache-tomcat-9.0.43.zip** para descargar tomcat, una vez realizada la misma descomprimimos el archivo con el comando**unzip apache-tomcat-*.zip** y lo movemos a la direccion **sudo mv apache-tomcat-*/ /opt/tomcat/**.

Ahora hay que dar permisos a los usuarios al irectorio de tomcat:

-	**Sudo chown –R tomcat: /opt/tomcat**
-	**Sudo chmod +x /opt/tomcat/latest/bin/*.sh.**

Despues hay que crear un archivo de unidad para ejecutar tomcat como servicio.

-	**Sudo nano /etc/systemd/system/tomcat.service**

### Al archivo credo le introducimos lo siguiente:

[Unit]
Description=Tomcat 9 servlet container
After=network.target
 [Service]
Type=forking
User=tomcat
Group=tomcat
Environment="JAVA_HOME=/usr/lib/jvm/default-java"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"
 
Environment="CATALINA_BASE=/opt/tomcat/latest"
Environment="CATALINA_HOME=/opt/tomcat/latest"
Environment="CATALINA_PID=/opt/tomcat/latest/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
ExecStart=/opt/tomcat/latest/bin/startup.sh
ExecStop=/opt/tomcat/latest/bin/shutdown.sh 
[Install]
WantedBy=multi-user.target

Usamos el comando **sudo systemctl start tomcat** y despues ejecutamos el mismo con el comando **sudo systemctlstatus tomcat** y para hacer que se ejecute de manera automatica usamos **sudo systemctl enable tomcat**.

### FIREWALL

Abrimos el puerto 8080 con el comando **sudo ufw allow 8080/tcp

###CONFIGURACION TOMCAT WEB MANAGER INTERFCE

Usamos **sudo nano /opt/tomcat/latest/conf/tomcat-users.xml**
una vez dentro del mismo peamos al final el usuario 

role rolename="admin-gui"
role rolename="manager-gui"
user username="daniel" password="daniel" roles="admin-gui,manager-gui"

Para acceder de manera remota nos metemos en **sudo nano /opt/tomcat/latest/webapp/manager/META-INF** y el código **Sudo nano /opt/tomcat/latest/webapp/host- manager/META-INF**

Comentamos dentro de ellos las direcciones IP.

### INSTALAR SSH

Lo iniciamos con **sudo systemctl start sshd.service** y vemos el estado con **sudo systemctl status sshd.service** y para modificar el puerto usamos **sudo nano /etc/ssh/sshd_config.**

### INSTALAR MARIADB

Para instalar usamos el comando **sudo apt install mariadb-server**.

Despues tenemos que usar el comando **sudo apt install mariadb-client**
Luego lo iniciamos CON EL COMANDO **sudo systemctl start mariadb** y hacemso que se ejecute de manera automativa **sudo systemctl enable mariadb** y para ver si esta conectado lo probamos con **systemctl status mariadb**


