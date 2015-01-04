# Introducción

Este repositorio contiene un ejemplo del fichero de configuración [fig](http://www.fig.sh/index.html) para instanciar MySQL (servicio de Base de Datos). Está basado en el contenedor Docker [luispa/base-mysql](https://registry.hub.docker.com/u/luispa/base-mysql/) (GitHub [base-mysql](https://github.com/LuisPalacios/base-mysql)). Mi contenedor está basado en el oficial [aquí](https://registry.hub.docker.com/_/mysql/) y [aquí](https://github.com/docker-library/mysql).

Un ejemplo de uso, montar otro contenedor con WordPress ([luispa/base-wordpress](https://registry.hub.docker.com/u/luispa/base-wordpress/)) y tener independiente la base de datos del servidor web. 

Consulta este [apunte técnico sobre varios servicios en contenedores Docker](http://www.luispa.com/?p=172) para ver más ejemplos de uso. 


## Ejecución con "fig"

Para automatizar con el programa [fig](http://www.fig.sh/index.html) y que arranquen el contenedor descarga y renombra el fichero fig-template.yml, modifica las variables y ejecuta el programa: 

    $ git clone https://github.com/LuisPalacios/servicio-db-log.git
    :
    $ mv fig-template.yml fig.yml   (edita a tu gusto)
    :
    $ fig up -d


# Personalización

La primera vez que arranques el contenedor es muy importante porque analizará si es necesario crear la estructura MySQL en el Volumen. Si lo encuentra vacío la creará y la contraseña de root será la que indiquemos en la variable MYSQL_ROOT_PASSWORD. Si por el contrario encuentra una estructura ya existente entonces la utilizará.


### Volumen

Directorio persistente para la estructura MySQL, debe apuntar a un directorio de tu HOST (/Apps/data/blog/db/mysql) que se montará en el contenedor como /var/lib/mysql.

   - "/Apps/data/blog/db/mysql:/var/lib/mysql"  


### Variable: MYSQL_ROOT_PASSWORD

Contraseña del usuario "root" que se asignará a MySQL si descubre el directorio vacío y necesita crear la estructura inicial. 


### Puertos

Este servicio expone el puerto 33001 para acceder a MySQL. Por defecto MySQL escucha en el puerto 3306, pero en mi caso lo he cambiado porque este fichero fig.yml lo utilizo junto con un servidor de WordPress y he decidido separar su base de datos y escuchar en un puerto concreto. Una vez más, es un ejemplo de uso, en tu caso podrás modificar el puerto a tu gusto. 

	- "33001" - Para que otro contenedor externo conecte con esta base de datos
	
