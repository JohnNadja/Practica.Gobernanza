# Prácticas de Gobernanza, Administración e Identidad con los servicios de Azure.
![azureAD](/images/azureAD.png)

## Índice
### [Introducción](#introducción)
### [Prerrequisitos](#prerrequisitos-para-las-prácticas)
### [Práctica con Azure Policy](#práctica-directivas) 
### [Práctica con Azure BluePrints (Planos técnicos)](#práctica-blueprints)
### [Práctica Roles y permisos](#práctica-roles)
------

### Introducción

#### Identidad
En **Azure** se puede administrar las políticas de seguridad de una forma sencilla y eficiente. Las políticas de seguridad se pueden configurar para una gran variedad de aplicaciones y servicios. Esto quiere decir, se pueden administrar las autenticaciones y autorizaciones de una empresa o una organización. Como principio se tiene ***Active Directory*** ![icon-AAD](/images/icon-Azure-Active-Directory.svg) (es un servicio tipo [SaaS](https://azure.microsoft.com/es-emx/services/active-directory/)), que es el directorio de usuarios de Azure para poder gestionar los recursos, los roles y las políticas de seguridad, dependeiendo de la asignación de los roles.

Esto se puede gestionar para diferntes tipos de usuarios a través de diferentes *tokens* de seguridad como Facebook, Google, Twitter, etc. Esto se llama **Active Directory B2C** ![icon-AAD](/images/icon-Azure-AD-B2C.svg).

Otros aspectos de Administración de Azure son:
 - **Administración de Aplicaciones** ![icon-AAD](/images/10313-icon-service-Managed-Applications-Center.svg) que permite gestionar las aplicaciones que se puedan instalar en ciertos dispositivos.
 -  **Azure AD Connect**, que permite conectar una aplicación con Azure AD en donde sea con Microsoft y sincroniza los usuarios, pero no mantiene las cualidades o permisos de los usuarios.
 - **Inicio único de sesión (Single Sign-On)**, que permite que una aplicación pueda iniciar sesión en Azure con una cuenta de usuario de Azure con una sola solicitud de inicio de sesión.
 - **Administración de dispositivos**, que permite gestionar los dispositivos además de:
    - Conectarse a las aplicaciones si el dispostivo está autorizado o verificado.
    - Verificar que se ocupen los recursos de una o varias aplicaciones específicas.
 - **Autenticación Multifactor (2FA)**, que permite a un usuario autenticarse en Azure con una sola solicitud de inicio de sesión y una autenticación de dos factores. Este servicio está disponible desde el **plan P1** en Active Directory. (siempre es bueno mantenerlo activo). Este se basa en 3 elementos:
     - Algo que se tiene (propiedad): celular, correo electrónico, etc.
     - Algo que se conoce (saber): contraseña, pin, patrón de seguridad, etc.
     - Algo que es (ser): huellas dactilares, escáner de iris, características faciales, etc.

Azure cuenta con ciertas regiones especiales para sus implementaciones en la nube, tales como **Azure China 21 Vianet**, **Azure Goverment** y **Azure Germany**. Cada una de estas regiones tiene una configuración diferente para las políticas de seguridad. Para más información sobre las regiones especiales, consulte [la documentación](https://docs.microsoft.com/en-us/azure/virtual-machines/regions#special-azure-regions).


#### Gobernanza en Azure

La Gobernanza en Azure es una forma de administrar las políticas de seguridad (o reglas aplicadas) en Azure para poder ser utilizada.

Existe un método para adaptar la nube de Microsoft para Azure ([Microsoft Cloud Adoption Framework](https://azure.microsoft.com/es-mx/solutions/cloud-enablement/cloud-adoption-framework/#overview)) que permite guíar los procesos de migración a la nube en Azure.
![azureFramework](/images/Azure-framework-stages.png)

La ilustración anterior muestra las etapas de la migración a la nube de Microsoft Azure de forma simplificada.

#### Cumplimiento de la ley de Microsoft

Microsoft cuenta con directivas, leyes y reglas de cumplimiento para la seguridad de la nube. Algunas de éstas son:
    - [***Trust Center de Microsoft***](https://www.microsoft.com/en-us/trust-center?rtc%3D1), como Microsoft cumple la ley.
    - [***Ofertas de cumplimiento de Microsoft***](https://docs.microsoft.com/es-mx/compliance/regulatory/offering-home), como Microsoft ayuda a cumplir la ley del usuario.
    - [***Delcaración de privacidad de Microsoft***](https://privacy.microsoft.com/es-MX/privacystatement), como Microsoft protege la privacidad y trata de datos de los usuarios.
    - [***Data Protection Addendum***](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA), como Microsoft protege los datos de usuario.
    - [***Aure Compliance Docuemntation***](https://docs.microsoft.com/es-mx/azure/compliance/), la documentación de cumplimiento de Azure.

#### Azure Directivas (o Azure Policy)

Este servicio permite implementar y/o crear directivas (reglas) para poder gestionar la nube de forma correcta.Las directivas son importantes para el cumplimiento de la ley. Los ***[ámbitos](https://docs.microsoft.com/es-mx/azure/governance/policy/concepts/scope)*** de las directivas son:
    - **Global**: se aplican a todos los servicios y aplicaciones.
    - **Service**: se aplican a los servicios.
    - **Application**: se aplican a las aplicaciones.

En otras palabras, ***el ámbito*** puede ser una cuenta,suscripción o grupo de recursos.

#### Azure BluePrints

Es un conjunto de iniciativas que automatizan la aplicación de iniciativas o directivas en Azure para ciertas suscripciones, grupos de recursos o cuentas.


----

### Prerrequisitos para las prácticas
 - Tener una cuenta de Azure para realizar la práctica en su [*Portal*](https://portal.azure.com/#home) (si aún no se cuenta con alguna, se puede hacer el registro en el siguiente [*enlace*](https://azure.microsoft.com/es-mx/free/)). 
 - Contar con una suscripción activa de Azure para poder realizar la práctica (en el enlace anterior se muestra como se puede hacer).
 - Contar con un *Grupo de recursos* en Azure. Si no se cuenta con alguno, se puede crear en el [Portal](https://portal.azure.com/#home) de Azure con los parámetros básicos:

    |Nombre|Descripción|
    |:-:|:-:|
    |Suscripción|Suscripción de Azure activa.|
    |Grupo de recursos|Nombre del grupo de recrusos.|
    |Region|Región de Azure donde se añojará el grupo de recrusos.|
----

 ### Práctica Directivas

 #### Instrucciones 

 1. En el [portal de Azure](https://portal.azure.com/#home) se busca el recurso **Directiva**. Se puede observar en vista general una interfaz con diversas opciones para gestionar las directivas (o ***reglas***), admás de vistas gráficas de qué operaciones están ocurriendo. Muestra la lista de directivas que son compatibles y también no compatibles. Dependiendo de la jerarquía de la organización, es como se encontrarán disponibles las directivas. Algunas directivas tienen dependencias.
![infoDirectivas](/images/infoDirectivas.gif)

 2. En **Eventos** (se encuentra en el panel lateral izquierdo del recurso), se enlistan qué directiva se ha cumplido o cuál no. 
![eventos](/images/eventos.png)

3. Para definir una directiva (regla) y asignarla, se debe ir al apartado ***Creación*** ➡ ***Definiciones***. Hay dos opciones: **Definición de directiva** (regla) o **Definición de iniciativa** (conjunto de reglas). 
Se selecciona la opción **Definición de directiva**.
    - Parámetros de Aspectos básicos:
        |Nombre|Descripción|
        |:-:|:-:|
        |Ubicación de definición|Es en donde se asignará la directiva nueva a la suscripción deseada (puede ser para toda la cuenta, pero dependerá de la jerarquía de la organización).|
        |Nombre| Nombre de la directiva. Ejemplo: "DirectivaUbicación".|
        |Descripción|Descripción de la directiva. Ejemplo: No puede ser creado ninún recurso fuera de la región Norteamericana.|
        |Categoría|Categoría de la directiva. Elegir **Crear nuevo**.|
    
    - Se pulsa el botón de **Guardar**.

    ![definicionDirectiva](/images/definicionDirectiva.gif)

    - Una vez creada la nueva directiva, ésta se puede editar si asi se desea.

2. Si se quiere asignar la directiva que, para este caso, será para el grupo de recursos creado en los ***requisitos***. Se irá al apartado ***Creación*** ➡ **Asiganaciones** u se pulsa el botón ***Asignar directiva***:
    - En ***Aspectos básicos***:
        |Nombre|Descripción|
        |:-:|:-:|
        |Ámbito|Seleccionar el grupo de recursos creado para esta práctica.|
        |Exclusiones|No se puede asignar la directiva en algún recurso específico (en esta práctica no se realizará).|
        |Definición de directiva|Seleccionar la directiva de **Ubicaciones permitidas** (se puede encontrar usando el cuadro de búsqueda).|

    - En ***Parámteros***:
        |Nombre|Descripción|
        |:-:|:-:|
        |Ubicación permitida|Seleccionar la ubicación deseada para sólo permitir en tales ubicaciones crear recursos que, para la descripción de la directiva, se indica que sólo deben ser en Norteamérica.|
    
    - En ***Mensajes de no cumplimiento***:
        |Nombre|Descripción|
        |:-:|:-:|
        |Mensaje de no cumplimiento|Redactar un mensaje de no cumplimiento para la directiva. Este mensaje se mostrará en el panel de eventos cuando se intente crear un recurso dentro del *Grupo de recursos* fuera de las regiones permitidas.|

    - Se pulsa el botón de **Revisar y Crear** y **Crear** para finalizar la creación de la directiva.
    ![asignarDirectiva](/images/asignarDirectiva.gif)

5. Para verficar que la directiva esté funcionando correctamente, se puede crear un recurso en el *Grupo de recursos* creado en los requisitos. Ejemplo rápido, un **[App Service](https://portal.azure.com/#view/HubsExtension/BrowseResource/resourceType/Microsoft.Web%2Fsites)**. Para fines de práctica, se tomarán en cuenta los siguientes aspectos:
    - En **Aspectos básicos**:
        |Nombre|Descripción|
        |:-:|:-:|
        |Susciprción|Seleccionar la suscripción de Azure activa.|
        |Grupo de recursos|Seleccionar el grupo de recursos creado para esta práctica.|
        |Nombre|Nombre del recurso. Ejemplo: "AppServiceForDirective".|
        |Publicar| Seleccionar **código**.|
        |Pila de entorno|Seleccionar cualquiera.|
        |Región| Seleccionar alguna región que sea **diferente** de Norteamérica.|

    - Se pulsa el botón de **Revisar y Crear** y **Crear** para finalizar la creación del recurso.
    ![crearAppService](/images/crearAppService.gif)

    - Se puede observar que el recurso no se ha creado correctamente porque la región no se encuentra en las regiones permitidas. Para arreglarlo, se debe crear de nuevo el recurso y seleccionar alguna región que se definió para poder implementar dentro del grupo de recursos.
    ![godAppService](/images/godAppService.gif)

    - Se puede observar que el recurso se ha creado correctamente.

6. Para crear una iniciativa (grupo de directivas o reglas), se debe ir al apartado ***Creación*** ➡ **Asignaciones** del recurso de Directiva. Se selecciona el botón ***Asignar directiva*** y el proceso es casi similar al de la directiva.

[⚠](#⚠importante⚠)
----

### Práctica BluePrints

#### Instrucciones

1. Se busca en el [portal de Azure](https://portal.azure.com) el recurso *Planos técnicos* para poder crearlo. Puede crearse uno desde cero o tomar una plantilla (que es justo lo que se realizará en esta práctica).
    - Se tomará la plantilla de **ISO 27001**. en ***Aspectos básicos***:
        | Nombre | Descripción |
        |:-:|:-:|
        | Nombre del plano técnico | Nombre del plano técnico. Ejemplo: "planotecnico27001".|
        |Ubicación de definición| Seleccionar la ubicación de definición de la plantilla. Ésta será la **suscripción activa**.|
    
    - En ***Artefactos*** son las ubicaciones, permisos, etc, que se implementará de acuerdo con el plano técnico.
    
    - Se selecciona **Guardar Borrador** y, si se desea, se puede crear una versión final del plano técnico pulsando el plano técnico y después el botón ***Publicar plano técnico**.
        |Nombre|Descripción|
        |:-:|:-:|
        |Versión|Colocar alguna versión que vaya de acuerdo con el plano. En este caso sería la versión ***1.0***|

    - Seleccionar **Publicar**. 
        ![crearPlanoTecnico](/images/crearPlanoTecnico.gif)

2. Una vez publicado el plano técnico, se debe **asignar** a la suscripción. Para ello, se selecciona el plano técnico y se pulsa el botón ***Asignar plano técnico***.
    - En **Asignación de bloqueo**, se puede elegir. Puede ser:
        - No bloquear
        - No eliminar
        - Sólo lectura

    - Se pulsa **Aceptar**.
    (**Nota**: algunos planos técnicos requieren aprobación si hay una jerarquía superior en la organización.)
    ![asignarPlanoTecnico](/images/asignarPlanoTecnico.gif)

[⚠](#⚠importante⚠)

----
### Práctica Roles

(**Nota**: se puede crear un rol para cada directiva, pero se recomienda crear un rol para todas las directivas y asignarlo a todas las directivas. Además, esta práctica está dirigida principalmente cuando se tenga una organización con una jerarquía de roles).

#### Instrucciones
Para esta práctica, se compartirá un grupo de recursos a otro integrante de una organización para que pueda tener tanto acceso, como edición de éste.

1. En **Control de acceso** (***IAM***) del grupo de recursos, seleccionar el botón ***Aregar*** ➡ *** Agregar asignación de roles***.
    - En **Rol**, se selecciona el rol que se quiere asignar para el nuevo miembro.
    - En **Miembros**, se selecciona (buscando) el miembro que se quiere asignar el rol.

    - Se **Revisa y asigna** el rol.

    ![asignarRol](/images/asignarRol.gif)

    - Para revisar que haya funcionado correctamente, el miembro debe revisar en su grupo de recrusos que tenga dicho grupo de recursos asignado.

[⚠](#⚠importante⚠)

-----

# **⚠Importante⚠** 

### Recordar que, si no se requiere más del servicio, se puede eliminar pulsando el botón **Detener** después de haber seleccionado la *instancia de proceso* que, se encuentra en **Proceso** del panel izquierdo.
O bien, eliminar el grupo de recursos dentro del [Portal de Azure](https://portal.azure.com/) si no se requiere todo el contenido de dicho grupo.

----
###### <sub>[Volver al índice principal de prácticas](#índice)<sub>

## Hasta aquí la finalización de las prácticas.