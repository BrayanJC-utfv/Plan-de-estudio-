Respuestas dudas semana 1 - Boundary rules e imports entre apps/libs

Caso 1: Aplicación consumiendo una Librería Permitida (Correcto)
Las aplicaciones pueden consumir sin restricciones las capacidades compartidas expuestas por los entrypoints públicos de las librerías.

┌──────────────────────────┐          ┌──────────────────────────┐
│      apps/workspace      │─────────►│     libs/shared/ui       │
│  (Aplicación Ejecutable) │  import  │  (Capacidad Compartida)  │
└──────────────────────────┘          └──────────────────────────┘

Caso 2: Aplicacion importado otra aplicacion (incorrecto)
las aplicaciones jamas deben invadir el directorio interno de otra aplicacion mediante rutas relativas cruzadaas 

┌──────────────────────────┐          ┌──────────────────────────┐
│       apps/shell         │── ── ── ►│       apps/portal        │
│  (Aplicación Ejecutable) │  import  │ (Código Interno/Privado) │
└──────────────────────────┘  CRUZADO └──────────────────────────┘

Caso 3: Host cargando un remote por superficie publica (correcto)
En module federation, la intercomunicacion entre aplicaciones se realizan exclusivamnete en tiempo de ejecucion a traves de los endpoints o rutas que el remoto expone publicamnete, nunca mediante complicacion estatica

┌──────────────────────────┐                  ┌──────────────────────────┐
│       apps/shell         │                  │       apps/portal        │
│         (Host)           │                  │         (Remote)         │
└─────────────┬────────────┘                  └─────────────▲────────────┘
              │                                             │
              │ Carga dinámica en tiempo de ejecución       │
              └─────────────────────────────────────────────┘
                         (Superficie Pública / Ruta)

**Ejemplos de uso de librerias y superficie publica (Correctos)**

1. Consumir componentes a través de Path Aliases de librerías:
Se consume un componnete UI generico desde el entrypoint publico de la libreria 
    SharedButtonComponent } from '@monorepo/shared/ui';

2. Consumir lógica de datos/servicios centralizada:
El servicio de autenticación global fue extraído a una capa compartida
    import { AuthService } from '@monorepo/shared/services';

3. Host montando dinámicamente un módulo remoto (Module Federation):
Carga perezosa (lazy loading) por mapeo de rutas, sin imports directos a archivos
    const routes = [
      {
        path: 'portal',
        loadChildren: () => import('portal/Module').then(m => m.PortalModule)
      }
    ];

--Ejemplos de acoplamientos destructivos (incorrectos)--

1. Importar un componente UI directamente desde otra app:
Invade el espacio de trabajo de 'portal' desde la aplicación 'workspace'
    import { NavbarComponent } from '../../portal/src/app/components/navbar/navbar.component';

2. Importar un servicio HTTP o lógica de API interna de otra app:
'security' intenta reutilizar un servicio de autenticación directo de 'shell'
    import { AuthService } from '../../shell/src/app/core/services/auth.service';

3. Importar un estado de sesión o interfaz compartida de forma cruzada:
'infinity' lee interfaces o tipados internos de la aplicación 'security'
    import { UserSession } from '../../security/src/app/models/user-session.interface';


**Tabla de evaluacion de fronteras arquitectonicas**

|─────────────────|────────────|──────────────────────────|─────────────────────────|
| Caso            | Permitido  | Por que                  | Alternativas            |
| ────────────────|────────────|──────────────────────────|─────────────────────────|
| App consume lib | si         | las librerias en libs/   | se mantiene el import   | 
|                 |            | estan diseñadas especifi | apuntando el path alias |
|                 |            | cas para proveer capacida| configurado             |
|                 |            | des y logica reutilizable|                         |
|                 |            | a cualquier app del espac|                         |
|                 |            | io de trabajo            |                         |
|─────────────────|────────────|──────────────────────────|─────────────────────────|
| App importar app| No         | Rompope el principio de  | extraer el componete    |
|                 |            | despliegue independiente | tipo o funcion          |
|                 |            | si la app destino cambia | compartida hacia una    |
|                 |            | su estructura. interna   | nueva libreria dentro   |
|                 |            | o se elimina la app      | de libs/                |
|─────────────────|────────────|──────────────────────────|─────────────────────────|
| Host monta      | Si         | es el flujo nativo       | configurar correctamnete|
| remote          |            | de module federation     | las propiedades remotes |
|                 |            | El host delega el control| en el el archivo        | 
|                 |            | de la rutasin conocer    | webpack.config o similar|
|                 |            | ni comppilar sus archivos| del host                |
|                 |            | internos                 |                         |
|─────────────────|────────────|──────────────────────────|─────────────────────────|


**¿Que moveria a libs/ui, libs/services, libs/state o libs/util?**

1. libs/ui
    Botones personalizados, modales genéricos, tablas dinámicas, layouts de tarjetas, menús de navegación o spinners de carga.

2. libs/services
    Clases de servicios HTTP de Angular, clientes Axios, configuraciones de endpoints de API o interceptores compartidos.

3. libs/state
    Selectores, acciones y reducers de NgRx, señales de Angular globales, configuraciones de almacenamiento para tokens o Stores de estado compartido.

4. libs/util
    alidadores personalizados de formularios, funciones puras de conversión (ej: formatear fechas o monedas), constantes globales del sistema, pipes de Angular reutilizables o guards de rutas.