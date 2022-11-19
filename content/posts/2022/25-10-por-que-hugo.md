---
title: "¿Por Qué Hugo Framework?"
date: 2022-10-25


categories:
- walkthrough
- guides

tags:
- hugo
- web-dessign

keywords:
- disqus
- google
- gravatar
autoThumbnailImage: false
thumbnailImagePosition: "top"
thumbnailImage: //www.michaelbromley.co.uk/media/2017/07/hugo-logo.png

metaAlignment: left
---
Porque elegir Hugo entre otros CMS y frameworks.
<!--more-->

{{< toc >}}

## El problema


La idea inicial era usar WordPress como gestor de contenidos para una landing page de presentación, y además incluir en el mismo sitio una sección de documentación.

Uno de los mayores retrasos a la hora de subir código a github es crear una documentación clara. Si además de la documentación del propio repositorio queremos llevar un registro paralelo, por ejemplo está web, nos topamos con el inconveniente de tener de escribir dos veces la misma documentación, una para el repositorio y luego adaptarla para la web general

## Dos pajaros de un tiro

Buscando alternativas para solventar este inconveniente me topé con Hugo Framework, un creador de sitios hecho en Go, con un workflow muy sencillo. Luego de elegir la plantilla o tema, simple se colocan en el directorio de contenidos los posts o entradas. Luego el Framework crea un render estático en HTML y CSS. Es ideal para sitios que no requieran componentes dinámicos ya que consume muy pocos recursos y las entradas se crean fácilmente en lenguaje Markdown, casualmente el mismo que utiliza GitHub para sus archivos README. De esta manera, en un solo paso estamos creando la entrada en la web dedicada, y la documentación para el repositorio

## Implementación 

Hugo Framewrok en su documentación oficial muestra distintas formas de instalación como compilar desde código fuente, binarios para Windows, mediante gestores de paquetes como HomeBrew o APT y mi versión elegida, mediante un contenedor de Docker. Si bien no está oficialmente mantenido por los creadores (se agradece a [Erlend Klakegg Bergheim](https://github.com/klakegg) por el trabajo), el sitio lo contempla como instalación estable.

### Despliegue del contenedor

La imagen creada por (se agradece a [Klakegg](https://github.com/klakegg) integra todo lo que se necesita para correr el servidor Hugo, solo hace falta montar dentro de la imagen el directorio con los archivos fuente (que la misma imagen también crea) y el contenido, tanto posts como imágenes. Dentro del repo de la misma también se encuentra el comando para correr el servidor directo en consola y también la plantilla para crear un archivo de Docker Compose.

### Workflow

El workflow o flujo de trabajo es bastante sencillo, los artículos son escritos en mi computadora personal, al terminar la edición los cambios son guardados y cargados en el repositorio de GitHub. Desde el lado servidor, hay un servicio que diariamente verifica que los archivos cargados en el servidor estén al día con los cambios hechos en el repositorio, en caso contrario se actualiza a los nuevos cambios y reinicia el servicio del servidor Hugo para hacer efectivos dichos cambios. De esta manera se evita que el contenido del servidor quede desactualizado por descuido.