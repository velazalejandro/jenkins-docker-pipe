# jenkins-docker-pipe

## Título
CI/CD con Jenkins + Docker / Dockerhub + GitHub

## Descripción
He desarrollado un pipeline combinando Jenkins + Docker + GitHub donde Jenkins automatiza la construcción, dockerización y despliegue de una aplicación web, simulando un entorno real de integración continua.

## 🛠️ Tecnologías utilizadas
-	GitHub para la creación de token, repositorio jenkins-docker-pipe para almacenar la estructura de carpetas y los archivos de configuración.
-	Jenkins versión 2.541.3 para configurar credenciales y crear el job pipeline.
-	Docker Desktop / Dockerhub para constuir imagen y crear token de acceso.
-	CMD o PowerShell para la ejecución de comandos.
-	Notepad para la creación de Dockerfile y Jenkinsfile.

## Estructura
01-pipeline: carpeta "src" --> contiene imágenes de la pagina
                      paginafutbol.html --> nuestra página web creada
                      Dockerfile --> para dockerizar y contruir nuestra imagen
                      Jenkinsfile --> para desplegar pipeline de la aplicación


## Pruebas ⚙️ y Despliegues 📦
1. Creamos el DockerFile y el Jenkinsfile.
2. Asegurarnos que Jenkins tiene Docker instalado. Instalamos plugins de Docker en Jenkins. Para ello seguimos la siguiente ruta:
Panel de Control – Administrar Jenkins – System Configuration – Plugins – Available plugins – Escribimos docker – Seleccionamos los 4 primeros plugins y los instalamos.

<img width="886" height="406" alt="image" src="https://github.com/user-attachments/assets/03b94c8b-22c9-40a9-91b2-4539563a04a1" />

