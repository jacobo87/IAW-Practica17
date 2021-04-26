# IAW - Práctica 17
>IES Celia Viñas (Almería) - Curso 2020/2021   
>Módulo: IAW - Implantación de Aplicaciones Web   
>Ciclo: CFGS Administración de Sistemas Informáticos en Red 

## Práctica 17: Balanceo de carga con HAProxy
Modificaremos los archivos ```docker-compose.yml``` que hemos creado en las prácticas 15 y 16, y vamos a incluir un nuevo contenedor Docker con HAProxy para balancear la carga de los contenedores que ejecutan la aplicación web.

## Escalar los servicios en un archivo ```docker-compose.yml```
Cuando ejecutamos docker-compose tenemos la posibilidad de indicar el número de instancias que queremos tener de cada uno de los servicios que vamos a crear.

El comando sería el siguiente:

```docker-compose up --scale SERVICE=NUM```

- SERVICE nombre del servicio a escalar.
- NUM número de instancias que queremos del servio.

## Ejemplo de un archivo ```docker-compose.yml``` con un balanceador de carga
Fragmento de un archivo ```docker-compose.yml``` que incluye un servicio de balanceo de carga con [HAProxy](http://www.haproxy.org/) que nos puede servir de ejemplo:
```bash
services:
  lb:
    image: dockercloud/haproxy <1>
    ports:
      - 80:80 <2>
      - 1936:1936 <3>
    links:
      - apache <4>
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock <5>

  apache:
    ...
```
## Archivo de configuración ```haproxy.cfg```
Parámetros del archivo de configuración de [HAProxy](http://www.haproxy.org/) es ```haproxy.cfg```.

Ejemplo de ```haproxy.cfg``` en el contenedor [docker](https://www.docker.com/)

## REFERENCIAS
- [José Juan Sánchez](https://josejuansanchez.org/iaw/practica-17/index.html)
- [Práctica 15 - Jacobo Azmani](https://github.com/jacobo87/IAW-Practica-Compose)
- [Práctica 16 - Jacobo Azmani](https://github.com/jacobo87/IAW-Practica16)
- [HAProxy Configuración](http://cbonte.github.io/haproxy-dconv/2.2/configuration.html)
- [Balancear un servicio web con HAProxy en Ubuntu](https://clouding.io/hc/es/articles/360010289000-Balancear-servicio-web-con-HAProxy-en-Ubuntu-18-04)