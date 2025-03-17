# devopsengineer2025-desafio 1
# Desafío #1 - Pipeline de Creación de Usuarios

Objetivo
Hice este pipeline en Jenkins para crear usuarios en un sistema Linux de forma automática. El área de seguridad me pidió esto porque hubo errores al dar de alta usuarios manualmente, y querían algo más confiable.

Escenario
El equipo de seguridad necesita gestionar usuarios en los sistemas de la empresa. Con este pipeline, pueden crear usuarios nuevos con sus datos y una contraseña temporal, que el usuario tiene que cambiar al entrar por primera vez.

Requisitos
- Datos de entrada:
  - Login: Se arma juntando el nombre y apellido.
  - Nombre y Apellido: Los datos del usuario.
  - Departamento: Puede ser "contabilidad", "finanzas" o "tecnologia" (los grupos ya tienen que existir en el sistema).
- Contraseña temporal: La genera el pipeline y la muestra para que el operador la copie y la mande por mail en archivo con nombre resultado.txt.
- Cambio de contraseña**: El usuario tiene que cambiarla al primer login.

Cómo usar el job
1. Configurar Jenkins:
   - Creá un job nuevo en Jenkins (yo lo llamé "Desafio1").
   - En "Pipeline", elegí "Pipeline script from SCM".
   - Puse el repositorio: `https://github.com/ezequieldureit/devopsit-desafios.git`.
   - En "Branch", puse `*/main`.
   - En "Script Path", puse `Pipelines/Jenkinsfile` (porque lo guardé en la carpeta Pipelines).
   - Usé mis credenciales de GitHub (las configuré en "Manage Credentials").

2. Ejecutar el job:
   - Hacé clic en "Build with Parameters".
   - Completá:
     - NAME: El nombre (ej: "Pedro").
     - LASTNAME: El apellido (ej: "Escamoso").
     - DEPARTMENT: Elegí uno de los tres (contabilidad, finanzas, tecnologia).
   - Dale a "Build".

3. Ver resultados:
   - En el log, vas a ver el login y la contraseña temporal.
   - Descargá el archivo `result.txt` desde "Archived Artifacts" para tener las credenciales o también podes hacer cat desde el bash de la ruta en este caso /var/lib/jenkins/workspace/Desafio1/result.txt

Prerrequisitos
- Jenkins instalado en Ubuntu.
- El usuario `jenkins` tiene que tener permisos `sudo` para `useradd` y `passwd`. Yo puse esto en `/etc/sudoers`:
