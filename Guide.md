# Google Apps Script Api

[Google Apps Script](https://developers.google.com/apps-script/overview) es una plataforma de desarrollo de Google para crear aplicaciones que interactuen con las aplicaciones de G Suite, tales como: Google Sheets, Google Docs, Google Forms, etc... Con Apps Script se pueden crear extensiones, macros, apis ejecutables, etc...

[Apps Script Api](https://developers.google.com/apps-script/api/) es una api de Google que permite administrar tus proyectos de Google Apps Script remotamente. Con esta api se pueden crear, actualizar, desplegar y ejecutar proyectos de App Script remotamente. 

La api de Apps Script se puede utilizar para administrar todas las etapas de un proyectos, o solo para administrar algunas de ellas, tal como el despliegue o la ejecucion de este. En esta guia solo se utilizara la api de Apps Script para ejecutar el proyecto remotamente, las demas etapas se implementaran utilizando el editor en linea de Apps Script.

## Crear un proyecto

Los proyectos de Apps Script se administran desde la página [G Suite Developer Hub](https://script.google.com/home). Desde esta página se puede crear un nuevo proyecto de Apps Script utilizando la opción **New script**. Al seleccionar esta opcion se abrira el editor de App Script desde el cual podras administrar todas las etapas de ese proyecto. 

Cuando se crea un proyecto de Apps Script, el proyecto se crea en un **Default Cloud Platform projects**. Este tipo de proyectos no permite desplegar los proyectos de Apps Script como una api ejecutable, lo cual es necesario para ejecutar el proyecto utilizando la api de Apps Script. Para poder desplegar el proyecto de Apps Script como una api ejecutable es necesario cambiar el tipo de proyecto de Google Cloud, lo cual se explica mas a delante.

Desde los proyectos de Apps Script se puede acceder a todas las apis de los servicios de G Suite, lo que permite por ejemplo, crear nuevos forms o leer las respuestas de estos. En esta [pagina](https://developers.google.com/apps-script/reference/forms/) se detalla como funciona la api de Google Form.

Despues de que tengas implementado el codigo que ejecutara tu proyecto, puedes pasar al despliegue de este.

## Desplegar el proyecto

Antes de desplegar un proyecto en App Script hay que asegurarse de agregar el siguiente código al manifest del proyecto (apps script.json). Esto es para poder ejecutar el proyecto remotamente utilizando la api de Apps Script.

```json
"executionApi": {
    "access": "DOMAIN"
}
```

Este archivo esta oculto por defecto, por lo que para hacerlo visible hay que ir a **View > Show manifest file**.

Despues hay que implementar el proyecto como una api ejecutable desde la opcion **Public > Deploy as API executable**. Si estas utilizando un **Default Cloud Platform** tendras que cambiar tu proyecto a un [Standard GCP project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects). Esto lo puedes hacer desde la opcion **Resources > Cloud Platform project**. Al seleccionar esta opcion se abrirá un cuadro de dialogo que te permitirá cambiar el tipo de proyecto. Para cambiar el tipo de proyecto introduce el numero del proyecto de GCP en el campo de texto y selecciona el boton **Set Project**. El numero del proyecto lo puedes encontrar en la configuración del proyecto de GCP. 

Despues de configurar el proyecto correctamente lo puedes desplegar como una api ejecutable. Despues de que el proyecto este desplegado correctamente puedes ejecutarlo remotamente utilizando la api de Apps Script.

## Ejecutar el proyecto con la api de Apps Script

Google posee librerias clientes para implementar la api de Apps Script desde diferentes plataformas. La siguiente [guía](https://developers.google.com/apps-script/api/quickstart/nodejs) explica como hacerlo desde Node js.

Despues de implementar el codigo de la guia, sutituye el codigo de la funcion `callAppsScript()` por el siguiente codigo: 

```javascript
script.scripts.run({
	'scriptId': 'id of the script to execute',
  'resource': {
  	'function': 'name of the function to run'
   }
}).then(res => {
    console.log('>>>>>>>')
    console.log(res.data)
    console.log('<<<<<<<<<')
})
```

El valor de `scriptId` es el id del proyecto de Apps Script. El id lo obtienes desde la opcion **File > Project prorperties**.

El valor de `function` es el nombre de la funcion que ejecutaras en el proyecto de Apps Script.

Ademas tienes que incluir el siguiente scope en el array Scopes `https://www.googleapis.com/auth/script.external_request`.

Y listo, esto es todo lo que necesitas para ejecutar un proyecto de Apps Script utilizando su api.

Para mas informacion sobre como ejecutar un proyecto de Apps Script utilizando la api de esta, visita la siguiente pagina [Executing Functions using the Apps Script API](https://developers.google.com/apps-script/api/how-tos/execute).

## Referencias

- https://developers.google.com/apps-script/

* https://developers.google.com/apps-script/guides/cloud-platform-projects#switch_to_a_different_google_cloud_platform_project

* https://developers.google.com/apps-script/api/concepts/

* https://script.google.com/home

* https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run

* https://github.com/google/clasp/blob/master/docs/run.md#run-a-function-that-requires-scopes





