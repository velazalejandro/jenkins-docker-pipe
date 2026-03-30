# jenkins-docker-pipe

## Título
CI/CD con Jenkins + Docker / Dockerhub + GitHub

## Descripción
He desarrollado un pipeline combinando Jenkins + Docker + GitHub donde Jenkins automatiza la construcción, dockerización y despliegue de una aplicación web, desde la integración del código hasta su despliegue en contenedores Docker, incluyendo gestión de credenciales y versionado de imágenes, simulando un entorno real de integración continua.

## Objetivos
- Automatizar el ciclo de build
- Empaquetar la aplicación en una imagen Docker
- Publicar imagen versionada
- Simular un flujo real de integración continua

## Arquitectura
GitHub → Jenkins → Docker Build → Docker Hub → Despliegue local

- GitHub → fuente del código
- Jenkins → orquestación CI/CD
- Docker → empaquetado
- Docker Hub → registro de imágenes
- Servidor / contenedor local → despliegue

## Flujo de la pipeline:
Pipeline declarativa SCM -> Docker Build -> Docker Login -> Docker Push -> Deploy

- Pipeline declarativa SCM: Definición de CI/CD escrita en Jenkinsfile (sintaxis declarativa) que se almacena y versiona en un sistema de control de versiones (git). Permite a Jenkins descargar automáticamente el script desde el repositorio antes de ejecutar las etapas de construcción, pruebas y despliegue.

- Docker Build: Se encarga de crear imágenes de Docker partiendo de un «contexto» y de un archivo de Dockerfile.
  
- Docker Login: Comando de la interfaz de línea de comandos (CLI) de Docker utilizado para autenticarse en un registro de imágenes (como Docker Hub), permitiendo guardar credenciales de forma segura. Es esencial para descargar (pull) imágenes privadas o subir (push) imágenes propias.
  
- Docker Push:
- Deploy: 

## 🛠️ Tecnologías utilizadas
-	GitHub para la creación de token, repositorio jenkins-docker-pipe para almacenar la estructura de carpetas y los archivos de configuración.
-	Jenkins versión 2.541.3 para configurar credenciales y crear el job pipeline.
-	Docker / Dockerhub para constuir imagen y crear token de acceso.
-	CMD o PowerShell para la ejecución de comandos.
-	Notepad para la creación de Dockerfile y Jenkinsfile.

## Estructura del directorio
01-pipeline: 
- carpeta "src" --> contiene imágenes de la pagina
- paginafutbol.html --> nuestra página web creada
- Dockerfile --> para dockerizar y contruir nuestra imagen
- Jenkinsfile --> para desplegar pipeline de la aplicación


## Ejecuciones paso a paso - Pruebas ⚙️ y Despliegues 📦
1. Creamos el DockerFile y el Jenkinsfile.
2. Asegurarnos que Jenkins tiene Docker instalado. Instalamos plugins de Docker en Jenkins. Para ello seguimos la siguiente ruta:
Panel de Control – Administrar Jenkins – System Configuration – Plugins – Available plugins – Escribimos docker – Seleccionamos los 4 primeros plugins y los instalamos.

<img width="886" height="406" alt="image" src="https://github.com/user-attachments/assets/03b94c8b-22c9-40a9-91b2-4539563a04a1" />

3. Credenciales en Jenkins:
El siguiente paso será configurar credenciales:
Para ello nos situamos en Security – Credentials
Add Credentials

<img width="886" height="384" alt="image" src="https://github.com/user-attachments/assets/91001157-0d38-412b-8cd1-b1448323ac9f" />

Seleccionamos la opción Username with password.

<img width="642" height="681" alt="image" src="https://github.com/user-attachments/assets/d1874393-3093-4f44-b300-efc4a962274d" />

Username: velazalejandro
ID: dockerhub
Password: usamos el Token de Dockerhub – Para generar el token en Dockerhub: Vamos a Account Settings – Personal Access Tokens – Genera uno.
Una vez creado, copiamos el token en el password.

<img width="534" height="573" alt="image" src="https://github.com/user-attachments/assets/7a8d6eeb-99fd-4540-b739-091229faa506" />

Credenciales añadidas correctamente.

<img width="886" height="171" alt="image" src="https://github.com/user-attachments/assets/4324555d-0773-41cb-9d5a-f667eac89739" />

Nos logeamos en Docker Hub: 
docker login –u velazalejandro
password: copiamos el token generado anteriormente en dockerhub

<img width="873" height="228" alt="image" src="https://github.com/user-attachments/assets/d8d87ddd-6b65-43c2-a40a-fb62255fdff4" />

4. En Dockerhub hemos creado el repositorio llamado pagina_futbol.

<img width="886" height="233" alt="image" src="https://github.com/user-attachments/assets/cf546bc2-00a5-48fe-80d2-49dc981784d4" />

En la consola de PowerShell: nos situamos en la ruta del Jenkinsfile y ejecutamos el comando de docker build.

<img width="886" height="36" alt="image" src="https://github.com/user-attachments/assets/50ac4c2d-3f47-431d-b175-5da6ecbde130" />

<img width="886" height="336" alt="image" src="https://github.com/user-attachments/assets/7b882fe0-834a-45c3-a907-00f00bce6274" />

Se ha creado la imagen docker con el tag indicado.

<img width="886" height="80" alt="image" src="https://github.com/user-attachments/assets/ef643776-fc2b-43a2-8e5f-ea099b5dc18f" />

Después ejecutamos el comando de docker push.

<img width="886" height="39" alt="image" src="https://github.com/user-attachments/assets/37ff3ee8-47fb-4eed-9709-41de3eecbb78" />

<img width="886" height="255" alt="image" src="https://github.com/user-attachments/assets/f15b02df-03e9-4143-adf8-5e7461eb0eee" />



## Pasos para la configuración y el despliegue en Jenkins

5.	Nos situamos en el menú principal de Jenkins – Seleccionamos Nueva Tarea

<img width="303" height="289" alt="image" src="https://github.com/user-attachments/assets/5e7160a2-ccba-4a65-b863-08d4122dfecb" />

6.	Seleccionamos la opción Pipeline y le llamamos pagina_futbol – OK.

<img width="509" height="261" alt="image" src="https://github.com/user-attachments/assets/2051b566-3441-4b53-bf74-d0b40ac14788" />

7.	Configuration – Pipeline – Definition -- aquí seleccionamos la opción Pipeline script from SCM para el control de versiones – SCM Git.
Copiamos la URL del repositorio: https://github.com/velazalejandro/jenkins-docker-pipe.git

<img width="886" height="398" alt="image" src="https://github.com/user-attachments/assets/bdb627f8-51fe-48b4-a9bf-caa16e865004" />

Añadimos la rama main que es la rama que viene por defecto en github.

<img width="886" height="227" alt="image" src="https://github.com/user-attachments/assets/251d2814-9145-4de1-8edc-e570113237eb" />

La ruta del script está situada en “01-pipeline/Jenkinsfile”. Aplicamos y guardamos.

<img width="369" height="303" alt="image" src="https://github.com/user-attachments/assets/377436fb-a06e-490b-b825-49b2375b6db7" />

Construir ahora para que así nos ejecute la pipeline.

<img width="886" height="386" alt="image" src="https://github.com/user-attachments/assets/e078f591-9dfc-4515-90a9-9dd149f68fcb" />

En la pestaña de Builds nos aparece la ejecución en progreso.

<img width="339" height="531" alt="image" src="https://github.com/user-attachments/assets/ba214120-5a69-4b66-b623-d7a51ccfb5ae" />

Finalmente ha funcionado la pipeline correctamente con todos los pasos realizados: docker build, docker login y docker push.

<img width="1336" height="403" alt="image" src="https://github.com/user-attachments/assets/9dbf8273-ed5c-44cf-a0e4-5071d09a2a35" />


## Licencia 📄
Bajo licencia GNU General Public License v3.0

## Autor
Alejandro Velaz

🎓 Formación: ASIR
