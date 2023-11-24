# 1. OBJETIVO

Dar a conocer las buenas prácticas a seguir en el uso de Git como herramienta para el manejo de versiones de los desarrollos almacenados en los repositorios.

# 2. ALCANCE

Esta documentación esta dirigida a las personas que hagan uso del repositorio en Git.

# 3. POLÍTICAS

Describa cualquier política o regla pertinente que deba seguirse en el contexto de esta documentación.

# 4. CONDICIONES GENERALES

Aquí se deben enumerar y explicar las condiciones generales que rigen la documentación.

# 5. ARTEFACTOS RELACIONADOS

Enlaces a los recursos relacionados.

| Repositorio |
|----------|
| [GitHub ACTSIS](https://github.com/ACTSIS/)    |

# 6. CONTENIDO

> [!IMPORTANT]
> Las palabras clave __"DEBE"__, __"NO DEBE"__, __"OBLIGATORIO"__, __"DEBERÁ"__, __"NO DEBERÁ"__, __"DEBERÍA"__, __"NO DEBERÍA"__, __"RECOMENDADO"__, __"PUEDE"__ y __"OPCIONAL"__ en este documento serán interpretadas como se describe en [RFC 2119-es](https://www.rfc-es.org/rfc/rfc2119-es.txt).

## Definir un flujo de trabajo

* Identificar las fases más relevantes en el ciclo de desarrollo.
* Precisar la manera de identificar los cambios en el proyecto.
* Establecer el procedimiento a seguir cuando sea necesario hacer cambios de emergencia.

Ejemplo:

* __Git Feature Branch Workflow__: Todas las características tienen una rama dedicada, en lugar de concentrar todo en master.

* __Gitflow Workflow__: Todas las entregas del proyecto tienen una rama dedicada, en lugar de concentrar todo en master.

* __Forking Workflow__: Cada persona que colabora tiene un repositorio propio, en lugar de uno centralizado.

El flujo de trabajo sería:

1. Se toma una tarea y se trabaja en ella
2. Se implementa pruebas unitarias propias
3. Se actualiza constantemente el repositorio local
4. Se publica la tarea
5. Se asegura que las pruebas unitarias y todas las pruebas de regresión pasen al servidor de compilación.
6. Se envía una solicitud de incorporación de cambios (`pull-request`)
7. Se revisa si el código contenido en la solicitud de incorporación de cambios (`pull-request`) es apto para integración y que todas las pruebas pasen correctamente, si todo está bien se integra automáticamente al servidor.
8. El administrador integra la solicitud que se crea y se implementa en la preparación para QA y UAT.
9. El servidor de compilación elimina la rama remota
10. Se borra la rama local

## Verificar el estado del repositorio

Al iniciar alguna operación, verifica el estado actual del repositorio (`git status`). Para obtener información de los cambios realizados, los archivos modificados y la rama en las que se encuentra.

Información obtenida:

* __Rama actual__: Nombre de la rama en qué se encuentra.
* __Cambios sin confirmar__: Listado de los archivos modificados que aún no se han confirmado.
* __Archivos preparados para la confirmación__: Listado de archivos que están en el área de preparación.
* __Archivos no rastreados__: Listado de archivos que no están siendo rastreados por Git.

Además, mostrará recomendaciones sobre los comandos que puedes ejecutar para manejar esos cambios. Por ejemplo, puede sugerir usar `git add` para agregar archivos modificados al área de preparación, o `git checkout` para descartar cambios en archivos específicos.

## Actualizar el repositorio local antes de hacer o enviar cambios

Para evitar conflictos ente archivos, antes de realizar o enviar algún cambio se recomienda obtener la más reciente actualización del repositorio remoto (`git pull`), con lo cual, ocurren dos operaciones principales__:

* __Descarga de cambios__: Esta operación (`git fetch`) descarga los cambios en tu repositorio local sin fusionarlos automáticamente con tu rama actual.

* __Fusión de cambios__: Después, esta operación (`git merge`) combina los cambios descargados con la rama local. Durante la fusión, Git intentará combinar los cambios automáticamente. En caso de haber conflictos, entre los cambios descargados y los cambios locales, Git los marcará y se requerirá resolverlos manualmente.

Antes de continuar con el trabajo, es importante revisar los cambios realizados después de la descarga, para cerciorarse que todo esté en orden, y evitar que nuestros cambios entren en conflicto con los cambios de otros miembros del equipo.

## Hacer confirmaciones frecuentes y significativas

Realiza confirmaciones (`git commit`) que representen una unidad lógica de cambios significativos. Esto facilitará la comprensión de los cambios realizados, mediante puntos de control periódicos, para deshacerlos si es necesario, así como la reducción del riesgo de conflicto entre dos cambios simultáneos.
Puedes hacer confirmaciones localmente en cualquier momento, y envíos (`git push`) cuando todo esté funcionando.

Entre las ventajas se tiene:

* __Claridad y comprensión de los cambios__: Ayuda a mantener un historial claro y coherente de los cambios realizados en tu repositorio.
* __Reversión y deshacer cambios__: Si vas a deshacer los cambios realizados, se facilita la selección del cambio a revertir.
* __Colaboración y trabajo en equipo__: Mejora la colaboración entre los miembros del equipo.
* __Claridad en los mensajes de confirmación__: Es importante proporcionar mensajes claros y descriptivos. Un buen mensaje tiene que ser conciso e informativo, explicando de manera sucinta qué cambios se realizaron y por qué.
* __Mantenimiento y gestión del código__: Facilita el mantenimiento y la gestión del código a largo plazo.

Los cambios en una confirmación, deben estar relacionados entre sí y tener un propósito común. Si realizó algunos cambios que pertenecen a diferentes aspectos o funcionalidades, así como si fueron demasiados, considera enviarlos en confirmaciones por separado, y con esto mantener la claridad y la coherencia.

Se recomienda realizar la confirmación de cambios terminados y probados, que además cumplan las normas y directrices de codificación del proyecto, evitando de esta manera, que estos puedan romper la compilación o causar errores en la aplicación.

## Buenas prácticas para un buen commit

Los mensajes proporcionan contexto e información de los cambios realizados. Por lo tanto, se tiene que proporcionar suficientes detalles acerca de los cambios realizados, permitiendo a otros miembros del equipo a entenderlos.

### Estructura

El mensaje de un commit se divide en 2 partes diferentes el __título__ y __cuerpo__ como se muestra en el siguiente ejemplo.

> [!NOTA]
> Se DEBE utilizar la siguiente estructura para los mensajes de los commits.

Ejemplo de estructura de un commit:

```json
 [Titulo] => REQ: Type: Subject
 
 [Body]
```

Como se observa en el ejemplo anterior, el título se conforma de dos partes las cuales son el *__Requerimiento__* y el *__tipo__* y el *__asunto__* del mensaje.

Ejemplo de comando en CLI:

```cli
git commit -m "REQ:XXXX ➕ADD: Se genera una nueva funcionalidad." -m "Se agregó funcionalidad botón Descargar Plantilla en la GEN_PLACAR"
```

### Type/ Tipo

El tipo de cambio que se realizó, se utiliza para identificar el propósito de la confirmación. Es RECOMENDADO utilizar los siguientes tipos de cambio:

| Tipo | Descripción |
|----------|----------|
| ➕ `ADD` | Agregar una nueva funcionalidad. |
| 🛠 `FIX` | Corregir un error. |
| 📚 `DOCS` | Cambios en la documentación. |
| 🚀 `DEPLOY` | Cambios en el despliegue. |
| 📦 `PKG` | Cambios en la configuración de paquetes. |
| ♻️ `REFACTOR` | Refactorización y mejoras. |
| 🧪 `TEST` | Cambios en las pruebas. |
| 🗑 `DELETE` | Se eliminan funciones o archivos. |
| 🚧 `WIP` | Trabajo en progreso. |
| 🎭 `MERGE` | Integración/Fusión. |
| ♾️ `DEVOPS` | Cambios en la integración o despliegue continuo y/o sistema de build. |
| 🎨 `STYLE` | Cambios de formato, tabulaciones, espacios, puntos y coma, etc.; no afectan al usuario. |

> [!IMPORTANT]
> Es importante notar que el *__Type__* se DEBE escribir en mayúsculas y se PUEDE utilizar un emoji para identificarlo.

### Subject/Asunto

El asunto no DEBE contener más de __50 caracteres__, y DEBE comenzar con una letra mayúscula y no terminar con un punto. Se DEBE utilizar el *imperativo* presente para describir lo que hace el commit, en lugar de lo que hizo y muy importante tenemos que acostumbrarnos a escribirlos en Inglés esto es una de las mejores prácticas que podemos tener. Por ejemplo, use __change__; no __changed__ o __changes__.

### Body/Cuerpo

Se utiliza para explicar el __¿Qué?__ y el __¿Por qué?__ de un commit, no el __¿Cómo?__. El cuerpo DEBE comenzar con una nueva línea después del asunto y DEBE limitarse a __72 caracteres__ por línea.

### Ejemplo

Tomando en cuenta las reglas anteriores, un ejemplo de un buen __commit__ sería:

> [!EXAMPLE]
> REQ:87360 📚DOCS: Redacción de reglas para commits
>
> En la sección Wiki se redactaron las buenas prácticas para los commits.

> [!IMPORTANT]
> Es RECOMENDADO generar __commit__ pequeños y frecuentes, en lugar de grandes y poco frecuentes, esto facilita la revisión de los cambios realizados.

## Utilizar ramas separadas y evita cambios directos en la rama principal (master/main)

Esto ayuda a mantener un flujo de trabajo organizado, facilitando además la colaboración con otros miembros del equipo y minimizando los riesgos de conflictos y errores.

* __Evita cambios directos a la rama principal__: Garantiza que el código en producción sea confiable y funcional. En su lugar, utiliza ramas separadas para realizar cambios y desarrollar nuevas características.
* __Utiliza ramas separadas para el desarrollo__: Aísla los cambios para trabajar en ellos de manera independiente, sin afectar directamente a la rama principal. Además, trabajar en ramas separadas facilita el seguimiento de los cambios y simplifica la colaboración con otros miembros del equipo.
* __Ramas con características separadas__: Evita interferencias con otros cambios en desarrollo, cuando se trabaja en una función o característica específica.
* __Fusión e integración__: Al finalizar el desarrollo y pruebas en una rama separada, incorpóralos a la rama principal de manera adecuada (`git merge`) (`git rebase`).

Con esta práctica, puedes minimizar los riesgos de conflictos y errores. Además, de facilitar la revisión y prueba de los cambios antes de que se integren con la rama principal, contribuyendo a la calidad y estabilidad del código.

## Añadir solo los archivos creados o ajustados

Evita añadir todos los archivos (`git add .`) ya que esto hace que se ingresen muchos archivos  innecesarios (*trash*), pudiendo repercutir gravemente en la dimensión del repositorio.

Añadir los archivos individualmente (`git add src/model/archivo.ext`) es la manera recomendada para cuidar el registro de gestión de cambios en el repositorio.

## No combinar o integrar dependencias, archivos binarios o generados

El repositorio tiene que ser exclusivamente para rastrear y administrar el código fuente con sus archivos relacionados, y NO DEBE almacenar archivos a los cuales no se les puede ajustar el código fuente. Además, la presencia de estos aumenta significativamente el tamaño del repositorio y pueden causar conflictos, dificultando de esta manera la colaboración en el desarrollo.

Consecuencia de incluir archivos binarios:

* __Conflictos y dificultades en la colaboración__: Ya que cambian cada vez que se generan.
* __Tamaño y rendimiento del repositorio__: Tienden a tener un tamaño mayor en comparación con los archivos de texto plano.
* __Reproducibilidad y mantenibilidad__: No hacen parte del código fuente principal, dificultando el mantenimiento de los mismos.

Para manejar adecuadamente estos archivos, siga estas prácticas__:

* __Utiliza `.gitignore`__: Permite especificar patrones de nombres de archivos o directorios que Git debe ignorar al realizar operaciones como `add` o `commit`.
* __Separar archivos generados de archivos fuente__: Almacena los archivos generados en un directorio separado y agrega el nombre al archivo `.gitignore`.
* __Proporcionar instrucciones de construcción__: En lugar de incluir los archivos binarios en el repositorio, proporciona instrucciones claras sobre cómo generar esos archivos a partir del código fuente y las dependencias necesarias.

## No incluya archivos personales

Evita confirmar archivos personales que contengan información sensible que no se comparte con otros miembros del equipo o almacenada en el repositorio de gestión de código fuente, por ejemplo, la configuración de la aplicación o las claves SSH. Comprueba al menos dos veces la confirmación, para asegurarse de que no contienen archivos personales.

> [!IMPORTANT]
> ¡No envíes tokens o claves de acceso a repositorios públicos! Si se hace, se recomienda revocarlos y generar nuevos.

## Lea la documentación de Git

Es la fuente de información precisa y confiable, que ayuda a utilizar Git de manera efectiva, resolver problemas y mantener un flujo de trabajo eficiente. Además, permitirá aprovechar al máximo esta poderosa herramienta de gestión de versiones.

* __La documentación oficial de Git__: Proporciona documentación completa, detallada y actualizada de aspectos, como, información sobre comandos, conceptos, configuraciones, flujos de trabajo, entre otros. Se recomienda empezar por la sección "*Git Basics*" para obtener una base sólida sobre los conceptos y comandos fundamentales.
* __Referencia de comandos__: Incluye una referencia completa de todos los comandos disponibles, con la respectiva descripción, opciones y cómo utilizarlo correctamente.
* __Manuales de Git__: Incluye varios manuales específicos sobre temas particulares. Algunos ejemplos son, Pro Git, Git Glossary, Git Hooks, Git Attributes, entre otros.
* __Ejemplos y tutoriales__: Además de la documentación técnica, también puede encontrar una sección de "*Git Tutorials*" con ejemplos prácticos y tutoriales paso a paso. Estos tutoriales cubren una amplia gama de temas, desde los conceptos básicos hasta flujos de trabajo avanzados, colaboración y más.
* __Explorando Git en la línea de comandos__: Utiliza la opción `--help` con cualquier comando para obtener información breve sobre su uso y opciones. Por ejemplo, ejecutando `git commit --help` se obtiene información sobre el comando `commit.`

> [!TIP]
> Hojas de trucos de Git: [Git Cheat Sheet](https://training.github.com/downloads/es_ES/github-git-cheat-sheet/)
