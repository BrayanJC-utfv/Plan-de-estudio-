Dia 2: arquitcetura y navegacion conceptal 

               ┌───────────────────────────┐
               │           shell           │
               │     (Host Principal)      │
               └─────────────┬─────────────┘
                             │
              Navegación por │ Ruta /app
              Ruta /infinity │
                             ▼
  ┌──────────────────────────┴┐     ┌──────────────────────────┐
  │          infinity         │     │        workspace         │
  │     (Remote Selector)     │     │  (Host Funcional/Remote) │
  └───────────────────────────┘     └────────────┬─────────────┘
                                                 │
                                   ┌─────────────┴─────────────┐
                                   │                           │
                                   ▼                           ▼
                     ┌──────────────────────────┐┌──────────────────────────┐
                     │           portal         ││          security        │
                     │     (Remote Funcional)   ││   (Remote de Seguridad)  │
                     └──────────────────────────┘└──────────────────────────┘

Aplicaciones (apps/)

 -shell: Host principal; punto de entrada (/login, /infinity, /app).
 -workspace: Host funcional intermedio para la ruta /app y también actúa como remote.
 -infinity: Remote que sirve como home o selector inicial tras el login.
 -portal: Remote funcional que resuelve lógicas de negocio.
 -security: Remote especializado en la administración y vistas de seguridad.

Librerías (libs/)

 -core / shared / util: Lógica base, helpers y utilidades comunes del sistema.
 -mf: Configuraciones y herramientas para la integración de Module Federation.
 -data-access / services / state: Consumo de APIs HTTP y manejo de estado global.
 -ui Componentes visuales reutilizables bajo el Sistema de Diseño.
 -i18n: Traducciones y soporte multi-idioma.
 -pwa: Configuración de Progressive Web App (Service Workers / offline).
 -testing: Mocks y utilidades centralizadas para pruebas unitarias.


Riesgos de Imports y Mitigación
 -Riesgo: Importar código interno de un remote desde otra aplicación. Si el remote cambia internamente, rompe las demás apps en runtime.
 -Mitigación:
  1. Consumir única y exclusivamente las superficies públicas expuestas (rutas y entrypoints oficiales del remote).
  2. Si dos aplicaciones necesitan compartir código, este se extrae obligatoriamente a una librería en libs/.
  3. Se automatiza la validación mediante la regla de ESLint @nx/enforce-module-boundaries para bloquear imports prohibidos en la terminal.