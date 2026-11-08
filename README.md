# entregable-1-cicd
 
Primer entregable del curso de CI/CD.
 
## Integrantes
 
Texto usado en `AUTOR`: `Danna Salazar`
 
| Nombre completo | Usuario de GitHub |
|---|---|
| Danna Salazar | dannx109 (propietaria del repositorio) |
 
## Ejecución exitosa del workflow
 
[Ver ejecución exitosa de `mi_workflow.yml`](https://github.com/actions/runner-images/issues/14748)
 
## Respuestas
 
### 1. ¿Qué eventos configuraste para disparar tu workflow y por qué?
 
Configuré dos eventos:
 
- **`push` a la rama `main`:** el workflow corre automáticamente cada vez que subo cambios a `main`. Así compruebo enseguida que mi automatización funciona sin hacer nada más.
- **`workflow_dispatch`:** permite ejecutarlo manualmente desde la pestaña Actions con el botón *Run workflow*. Sirve para repetir la ejecución cuando quiero, sin tener que hacer un commit nuevo.
### 2. ¿Qué sistema operativo utiliza el runner `ubuntu-latest` y por qué puede ejecutar tu workflow aunque tu computadora sea Windows o macOS? ¿Qué relación tiene el runner con el shell de los pasos `run`?
 
El runner `ubuntu-latest` usa **Ubuntu Linux**. Es una máquina virtual que GitHub crea en la nube para cada ejecución, así que los pasos del workflow no se ejecutan en mi computadora sino en esa máquina. Por eso no importa si mi computadora usa Windows o macOS: lo único que hago desde mi equipo es subir los archivos, y GitHub se encarga del resto.
 
El shell de los pasos `run` depende del sistema operativo del runner: en Ubuntu y macOS normalmente es Bash y en Windows es PowerShell. Por eso, si cambio de runner, los comandos pueden cambiar. En este taller usé Ubuntu y fijé `shell: bash` para que `$(date)` funcione siempre igual. La fecha que se imprime es la del runner, no la de mi computadora.
 
### 3. Tres acciones pre-construidas del Marketplace (no mencionadas en el material)
 
- **`actions/cache`:** guarda en caché archivos que se descargan seguido, como las dependencias de un proyecto, para que las siguientes ejecuciones sean más rápidas.
- **`docker/build-push-action`:** construye una imagen de Docker y la publica en un registro (por ejemplo Docker Hub). Se usa para empaquetar aplicaciones en contenedores.
- **`github/codeql-action`:** analiza el código en busca de vulnerabilidades de seguridad. Sirve para detectar problemas antes de que lleguen a producción.
### 4. ¿Qué es un secreto en GitHub Actions y para qué se usa? ¿Cómo lo usarías en tu workflow?
 
Un secreto es un valor sensible, como una contraseña, un token o una clave de acceso, que se guarda cifrado en GitHub fuera del código. Se usa para que el workflow pueda autenticarse en servicios externos sin escribir esas credenciales en el repositorio, donde cualquiera podría verlas.
 
Se crea en *Settings > Secrets and variables > Actions > New repository secret* y se usa dentro del workflow con una expresión como `${{ secrets.NOMBRE_DEL_SECRETO }}`. En este taller no necesité ninguno, pero si mi workflow tuviera que desplegar en un servicio en la nube, guardaría ahí la clave de acceso y la pasaría a la acción correspondiente con `with:`. Nunca debo imprimirlo en los logs.
 
### 5. Reflexión: ¿qué tareas automatizarías con GitHub Actions y por qué?
 
**Danna Salazar:**
 
1. *(ESCRIBE AQUÍ TU PRIMERA IDEA y por qué. Ejemplo: ejecutar pruebas automáticamente en cada push para detectar errores rápido en vez de descubrirlos tarde.)*
2. *(ESCRIBE AQUÍ TU SEGUNDA IDEA y por qué. Ejemplo: revisar el formato y la calidad del código en cada pull request para mantener un estilo consistente.)*
 
