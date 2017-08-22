---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-06-01"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Resolución de problemas de gestión de cuentas
{: #managingaccounts}

Los problemas generales con la gestión de la cuenta pueden incluir que distintas
apps compartan el mismo nombre de dominio o que los administradores no puedan ver
todas las organizaciones. En muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}

## No es posible acceder a otra región diferente de {{site.data.keyword.Bluemix_notm}}
{: #nosecondreg}

Se recibe un mensaje de error al intentar crear una nueva región de {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms}

Es probable que esto ocurra por estar utilizando una cuenta Estándar, que únicamente da soporte al desarrollo en una región pública. La región pública de {{site.data.keyword.Bluemix_notm}} en la que desea trabajar se elige cuando se configura la cuenta por primera vez. 
{: tsCauses}

Si tiene una cuenta Estándar, puede actualizarla a una cuenta facturable para acceder a más regiones. Vaya a la página **Gestionar > Facturación y utilización > Facturación** en la consola y, a continuación, pulse **Añadir tarjeta de crédito**. En la página **Facturación**, también puede comprobar si tiene una cuenta Estándar.
{: tsResolve}

## No es posible crear una nueva organización
{: #nosecondorg}
 
Recibe un mensaje de error al intentar crear una nueva organización. 
{: tsSymptoms}

Es probable que esto ocurra por estar utilizando una cuenta Estándar, que únicamente da soporte al desarrollo en una organización. La organización la crea cuando configura la cuenta por primera vez. 
{: tsCauses}

Si tiene una cuenta Estándar, puede actualizarla a una cuenta facturable para acceder a más organizaciones. Vaya a la página **Gestionar > Facturación y utilización > Facturación** en la consola y, a continuación, pulse **Añadir tarjeta de crédito**. En la página **Facturación**, también puede comprobar si tiene una cuenta Estándar.
{: tsResolve}

## No es posible crear una nueva instancia de plan Lite
{: #nosecondlite}

El siguiente mensaje de error se visualiza cuando intenta crear una nueva instancia de plan Lite:
{: tsSymptoms}

`No es posible aprovisionar una nueva instancia de Lite`

Hay un límite de una instancia de plan Lite para mantener estos planes gratuitos. 
{: tsCauses}

Es posible crear instancias adicionales del servicio seleccionando uno de los planes de servicios facturables, que también están disponibles en las cuentas facturables. Para actualizar a una cuenta facturable desde la consola, vaya a la página **Gestionar > Facturación y utilización > Facturación ** y, a continuación, pulse **Añadir tarjeta de crédito**.
{: tsResolve}

Si no desea actualizar la cuenta Estándar y ya no está utilizando la instancia de servicio Lite existente, puede suprimir dicha instancia de plan Lite desde el panel de control Servicios y, a continuación, crear una nueva instancia. 

## Se ha excedido la concesión de memoria de tiempo de ejecución
{: #noruntimemem}

No puede desplegar apps y aparece un error que indica que ha superado el límite de memoria de su organización.
{: tsSymptoms}

En una cuenta Estándar, sus apps de Cloud Foundry pueden utilizar hasta 256 MB de memoria de tiempo de ejecución instantánea. En las cuentas facturables, hay un límite de 2 GB de memoria.
{: tsCauses}

Si está utilizando una cuenta estándar, puede obtener memoria adicional actualizando a una cuenta facturable. Vaya a la página **Gestionar > Facturación y utilización > Facturación** en la consola y, a continuación, pulse **Añadir tarjeta de crédito**.
{: tsResolve}

Si no desea actualizar la cuenta Estándar y tiene apps desocupadas, puede suprimirlas para liberar memoria de tiempo de ejecución. 

## La cuenta está inactiva
{: #ts_accnt_inactive}

No puede crear una app en {{site.data.keyword.Bluemix_notm}} si la cuenta está inactiva. Debe ponerse en contacto con el equipo de soporte para solucionar este problema.

Cuando intenta crear una app en {{site.data.keyword.Bluemix_notm}}, ve el siguiente mensaje de error:
{: tsSymptoms} 

`BXNUI0096E: La app no se ha creado. La cuenta está inactiva porque se ha cancelado o suspendido.`

El estado de la cuenta de {{site.data.keyword.Bluemix_notm}} pasa a ser inactivo si la cuenta se cancela o se suspende.
{: tsCauses}


Para volver a activar la cuenta, póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://ibm.biz/bluemixsupport.com){: new_window}. Incluya la siguiente información en el correo electrónico:
{: tsResolve}

  * El ID de IBM que utiliza para iniciar la sesión en {{site.data.keyword.Bluemix_notm}}.
  * El nombre de la organización en la que se está creando la app. Esta información puede ayudar al equipo de soporte a determinar si se le han asignado los roles o pertenencia a grupos correctos en la organización.


## No hay espacio asociado a la organización actual
{: #ts_no_space}

No puede crear una app si no hay ningún espacio asociado a la organización actual.

Cuando intenta crear una app en {{site.data.keyword.Bluemix_notm}}, ve el siguiente mensaje de error:
{: tsSymptoms} 

`BXNUI0097E: Para poder añadir una app, al menos un espacio debe estar asociado con la organización y la región. En el Panel de control, pulse Crear un espacio. Cuando se cree el espacio, vuélvalo a intentar.`

Las apps de {{site.data.keyword.Bluemix_notm}} se deben crear en un espacio de la organización.
{: tsCauses} 

Para crear un espacio, utilice uno de estos métodos: 
{: tsResolve}
 
  * En el Panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione la organización en la que desea crear el espacio y pulse **Crear un espacio**.
  * En la interfaz de línea de mandatos cf, escriba `cf create-space <space_name> -o <organization_name>`.

  
## Las apps comparten el mismo nombre de dominio
{: #ts_domain_diff}

Puede que observe que varias apps comparten el mismo URL en {{site.data.keyword.Bluemix_notm}}.

Este problema puede producirse cuando se asigna la misma ruta de URL a distintas apps de un espacio.
{: tsCauses}

Por ejemplo, supongamos que envía la app myApp1 a {{site.data.keyword.Bluemix_notm}} y establece el dominio en "mynewapp.stage1.mybluemix.net". Luego envía otra app myApp2 al mismo espacio y establece una de sus rutas de URL en "mynewapp.stage1.mybluemix.net". Ahora la ruta está correlacionada a ambas apps.

Este es el comportamiento soportado de {{site.data.keyword.Bluemix_notm}} y puede utilizar este procedimiento para conseguir un tiempo de inactividad cero para la actualización de la app. Para obtener más información, consulte [Utilización del despliegue azul-verde para reducir el tiempo de inactividad y el riesgo ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}.
{: tsResolve}
  

## Los administradores no pueden ver todas las organizaciones utilizando la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}
{: #ts_ui_org}

Como administrador, al utilizar la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, no puede visualizar todas las organizaciones para administrarlas. Puede visualizar y administrar únicamente aquellas organizaciones a las que pertenezca.

Como administrador, no puede ver todas las organizaciones utilizando la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Se trata de una limitación de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Puede utilizar mandatos como `cf orgs`, `cf create-org` y `cf delete-org` desde la interfaz de línea de mandatos de cf para gestionar todas las organizaciones. Para ver una lista completa de mandatos de cf, especifique `cf help`.
{: tsResolve}
	
## La tarjeta de crédito no se puede agregar
{: #ts_addcc}

No puede enviar información de su tarjeta de crédito para convertir la cuenta de prueba en una cuenta de pago según uso.

El botón **Enviar** de la página Añadir tarjeta de crédito está inhabilitado.
{: tsSymptoms}

El problema se produce cuando no se ha rellenado la página Añadir tarjeta de crédito con información correcta.
{: tsCauses}


Siga estos pasos:
{: tsResolve}

  1. En la página Añadir tarjeta de crédito, rellene los campos necesarios de las secciones: información de contacto, dirección de contacto y dirección de facturación.
  2. Seleccione **He leído y acepto los términos y condiciones de IBM**, luego pulse **Enviar**. Se muestra la sección **Seleccionar un método de pago**.
  3. Escriba el número de tarjeta de crédito, la fecha de caducidad y el código de seguridad de su tarjeta. Luego pulse **Enviar**.
