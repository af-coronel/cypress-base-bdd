# Detalles del proyecto

Configuración basica de Cypress + Cucumber para realizar los ejercicios de "Desafíos"

# Índice

- [Cómo Comenzar](#cómo-comenzar)
  - [Instalación de dependencias](#instalación-de-dependencias)
  - [Ejecución de tests](#ejecución-de-tests)
- [Configuración de VSC](#configuración-de-VSC)
  - [Plugins recomendados para el VSCode](#plugins-recomendados-para-el-vscode)
  - [Navegar desde el feature al step](#navegar-desde-el-feature-al-step)
  - [Linting](#linting)
- [Proyecto](#proyecto)
  - [Estructura del Proyecto](#estructura-del-proyecto)
- [Documentación de Cypress y Cucumber](#documentación-de-cypress-y-cucumber)
- [Troubleshooting](#troubleshooting)

 
# Cómo Comenzar

## Instalación de dependencias

Luego de clonar o descargar el repositorio, emplear la consola/terminal y escribir:

> npm install

Se auto-generará una carpeta denominada "node-modules" con los archivos necesarios para poder ejecutar los tests.

## Ejecución de tests

Para correr los test de manera local, con ventana de ejecución, en la consola/terminal escribir:

> npx cypress open

# Configuración de VSC

## Plugins recomendados para el VSCode

En el caso de emplear el "Visual Studio Code", se recomienda ingresar al menú lateral de Extensiones o Plugins (icono de 4 cuadraditos) e instalar los siguientes plugins:

- **Better Comments**: aaron-bond.better-comments
- **Bracket Pair Colorization Toggler**: dzhavat.bracket-pair-toggler
- **Cucumber (Gherkin) Full Support**: alexkrechik.cucumberautocomplete
- **Cucumber Formatter**: telmodsg.cucumber-formatter
- **Cypress Helper**: shelex.vscode-cy-helper
- **Cypress Snippets**: andrew-codes.cypress-snippets
- **cypress-cucumber-steps**: dylanmoerland.cypress-cucumber-steps
- **ESLint**: dbaeumer.vscode-eslint
- **GitLens - Git supercharged**: eamodio.gitlens
- **Material Icon Theme**: PKief.material-icon-theme
- **Path Intellisense**: bracket-pair-toggler.run
- **PowerShell**: christian-kohler.path-intellisense
- **Prettier-Code formatter**: esbenp.prettier-vscode
- **Rainbow CSV**: mechatroner.rainbow-csv

## Navegar desde el feature al step

1. File > Preferences > Settings (Code > Preferences > Settings on Mac)
2. Hacer click en la pestaña **Workspace**
3. Click en el botón "Open Setting (JSON)" ubicado arriba a la derecha (hoja con flecha)
4. Verificar que la configuración sea la siguiente

```
{
    "workbench.settings.useSplitJSON": false,
    "cucumberautocomplete.steps": [
        "cypress/e2e/step_definitions/**.js"
      ],
   "cucumberautocomplete.syncfeatures": "cypress/e2e/features/**/*.feature",
   "cucumberautocomplete.strictGherkinCompletion": false,
   "cucumberautocomplete.smartSnippets": true,
   "cucumberautocomplete.stepsInvariants": true
}
```

Más información: [StackOverflow](https://stackoverflow.com/questions/66434401/is-it-possible-to-navigate-from-feature-file-to-step-definition-and-vice-versa-i?newreg=c766d9efea28417c949af597a9f8098b)

## Linting

Herramienta de **análisis estático** que permite realizar una revisión del código sin ejecutarlo.

Para configurarlo, se deben seguir los siguientes pasos:

1. En la parte inferior izquierda, presionar la "rueda"
2. En el menú, seleccionar **Settings**
3. En "Search settings" ingresar "format on save"
4. Activar el checkbox "Format a file on save. A formater..."
5. La primera vez que se guarde un archivo, aparecerá un menú con las opciones "Prettier", "TypeScript", etc. Seleccionar "Prettier - Code formatter"

# Proyecto

## Estructura del Proyecto

El proyecto contiene la siguiente estructura de carpetas:

- **cypress:** Carpeta principal del proyecto que contiene los tests escritos en Gherkin, page object, definición de los pasos.
  - **e2e**: Carpeta que contiene todos los tests end to end.
    - **features**: Carpeta que contiene todos los tests escritos en Gherkin
    - **step_definition:** Carpeta que contiene la definición de cada paso de los tests.
  - **fixtures:** Archivos json que contienen información para verificar en los tests (principalmente tests de servicio)
  - **pages:** Page object. Archivos con los locadores de los elementos necesarios en los tests.
  - **support:** Comandos genéricos necesarios para los tests, como por ejemplo, validar la respuesta de un servicio.
- **.gitignore**: Archivos o carpetas que no se desean versional
- **cypress.config.js:** Archivo que contiene la configuración de URL, dependecias y plugins.
- **package:** Listado de dependencias npm necesarias para el proyecto.
- **Readme:** Documentación principal del proyecto de automation.

## Configuraciones Básicas

[Configuración](https://docs.cypress.io/guides/references/configuration)

**cypress.config.js** es el archivo utilizado para guardar cualquier configuración específica de Cypress.

Se puede configurar:
- **specPattern:** Tipo de archivos que conforman las pruebas (.feature)
- **viewportWidth**: ancho predeterminado en px de la ventana. (por defecto 1000).
- **viewportHeight**: altura predeterminada en px de la ventana. (por defecto 660).
- **video:** Permite seleccionar si Cypress capturará un video de las pruebas ejecutadas durante el **run**.
- **reintentos:** Permite indicar la cantidad de veces que se debe volver a intentar ejecutar una prueba fallida. Se puede configurar individualmente la cantidad de intentos para **runMode** o modo de ejecucón y para **openMode** o modo ventana.
- **downloadsFolder:** Ruta a la carpeta donde se guardan los archivos descargados durante una prueba.
- **chromeWebSecurity:** Al desabilitarlo permite cargar sitios cuya url de origen es diferente de la url que se está testeando (muchas páginas emplean otros dominios para el login o imágenes por ejemplo).
- **trashAssetsBeforeRuns:** Permite determinar si Cypress eliminará los activos dentro de la carpeta de descargas, la carpeta de capturas de pantalla y la carpeta de videos antes de que se ejecuten las pruebas con cypress run.
- **defaultCommandTimeout:** Tiempo, en milisegundos, de espera hasta que la mayoría de los comandos basados en DOM se consideren agotados. (Por defecto era 4000)
- **defaultpageLoadTimeout:** Tiempo, en milisegundos, de espera hasta que se descarga la nueva página. (Por defecto era 4000).
- **experimentalMemoryManagement:** Habilita la compatibilidad con una gestión de memoria mejorada en los navegadores basados en Chromium.
- **testIsolation:** Las pruebas siempre deben poder ejecutarse independientemente unas de otras y aun así pasar. Para ello se sugiera que testIsolation sea **true**. Esta propiedad:
  - borra la página visitando about:blank
  - borra las cookies en todos los dominios
  - almacenamiento local en todos los dominios
  - almacenamiento de sesiones en todos los dominios
    Más info en [Cypress - Test Isolation](https://docs.cypress.io/guides/core-concepts/test-isolation#Test-Isolation-in-End-to-End-Testing)

# Documentación de Cypress y Cucumber

- [Documentación Oficial de Cypress](https://docs.cypress.io)
- [Configuración de Variables de Ambiente](https://docs.cypress.io/guides/guides/environment-variables#Setting)
- [Configuración Global](https://docs.cypress.io/guides/references/configuration#Global)
- [Ejemplo de Recetas de Cypress](https://github.com/cypress-io/cypress-example-recipes)
- [Documentación Oficial de Cucumber](https://cucumber.io/docs/gherkin/reference/)
- [Tablas en Cucumber](https://qamind.com/blog/hashes-rows-raw-rowshash-from-datatable-class/)
- [Full Journey - Como escribir BDD de historias largas](https://stackoverflow.com/questions/38785073/best-ways-to-write-bdd-for-long-stories)
- [Cucumber in Cypress: A step by step guide](https://filiphric.com/cucumber-in-cypress-a-step-by-step-guide)
- [Cypress: getAllLocalStorage](https://docs.cypress.io/api/commands/getalllocalstorage)
- [Cucumber Basics](https://github.com/badeball/cypress-cucumber-preprocessor/blob/master/docs/cucumber-basics.md)
- [Badeball documentation](https://github.com/badeball/cypress-cucumber-preprocessor/tree/master/docs)
- [How to save and restore state in Cypress tests](https://reflect.run/articles/how-to-save-and-restore-state-in-cypress-tests/)
- [Intercept 2 services](https://filiphric.com/how-to-wait-for-page-to-load-in-cypress)
- [Muting Noisy XHR Logs in Cypress](https://dev.to/samelawrence/muting-noisy-xhr-logs-in-cypress-4495)
- [Chrome crash](https://docs.cypress.io/guides/references/error-messages#The-Chromium-Renderer-process-just-crashed)
- [Tags Documentation](https://filiphric.com/cucumber-in-cypress-a-step-by-step-guide)
- [Cypress Image Diff Documentation](https://cypress.visual-image-diff.dev/getting-started)
- [Viewport Config](https://docs.cypress.io/api/commands/viewport)

# Troubleshooting

- **Problemas al realizar un "npm install"**
  Si al intentar instalar npm se visualiza el mensaje de error "Sonatype Nexus Repository Manager", se recomienda elminar el archivo **package-lock.json** y ejecutar `npm install` nuevamente.

- **Problemas de cache**
  Para eliminar la cache, ejecutar el comando `npx cypress cache clear` ó `npm cache clean --force` o ejecutar `npx cypress cache path` y eliminar ese folder manualmente
  Para verificar que el cache realmente fue eliminado ejecutar el comando `npx cypress cache list`
  Si los problemas con versiones viejas de cypress persisten, se puede emplear `npx cypress install --force`

- **Problemas al ejecutar los tests: Error: ENOENT: no such file or directory, stat ...**
  Puede que algunas versiones de nodeJS generen conflictos con versiones de dependencias. Se recomienda emplear node v20.x .En caso de necesitar varias versiones de node, se recomienda el software [nvm - Node Version Manager](https://github.com/nvm-sh/nvm) .Si empleando nvm en windows tienes problemas, emplea "Windows Power Shell" como administrador. Con `nvm list` asegurate de estar empleando la versión de node adecuada. De no ser así, emplea `nvm use XX.XX.X` para cambiar de versión. Si aún no instalaste la versión que necesitas, prueba emplear `nvm install XX.XX.X`
  Otra opción de descarga es https://github.com/coreybutler/nvm-windows/releases/tag/1.1.12

- **FATAL ERROR: Committing semi space failed. Allocation failed - JavaScript heap out of memory**
  https://www.makeuseof.com/javascript-heap-out-of-memory-error-fix/
