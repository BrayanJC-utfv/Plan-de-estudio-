Respuestas dudas semana 1 - ArGestion de estados globales compartidos en libs/state

1. Modal abierto / cerrado
    Tipo de estado: Local
    Ubicación: Componente (.ts / .component.ts)
    Justificación: Solo le interesa a la vista actual para controlar la UI reactiva. Desaparece cuando se desmonta el componente.
2. Token de sesión (JWT)
    Tipo de estado: Global Compartido
    Ubicación: libs/state
    Justificación: Es utilizado por varios microfrontends (shell, security) para autenticación, interceptores y validación de accesos.
3. Lista de usuarios desde API
    Tipo de estado: Servidor
    Ubicación: TanStack Query (libs/services)
    Justificación: Son datos remotos que requieren caché, sincronización e invalidación automática.
4. Tema claro / oscuro (Dark Mode)
    Tipo de estado: Global Compartido
    Ubicación: libs/state
    Justificación: Afecta la apariencia de todas las aplicaciones del monorepo.
5. Búsqueda escrita en una tabla
    Tipo de estado: Local
    Ubicación: Componente o Feature
    Justificación: Es un dato temporal utilizado únicamente para filtrar información en la pantalla actual.
6. Idioma activo (es / en)
    Tipo de estado: Global Compartido
    Ubicación: libs/state
    Justificación: Determina las traducciones y configuraciones de internacionalización en todos los microfrontends.
7. Datos del perfil del usuario
    Tipo de estado: Global Compartido
    Ubicación: libs/state
    Justificación: Información básica del usuario (nombre, foto, correo) utilizada en distintas aplicaciones y componentes compartidos.
8. Filtros temporales de una pantalla
    Tipo de estado: Local
    Ubicación: Componente o Feature
    Justificación: Son parámetros temporales que solo tienen sentido dentro de una pantalla específica.
9. Permisos del usuario
    Tipo de estado: Global Compartido
    Ubicación: libs/state
    Justificación: Son consultados por guards, directivas y componentes para controlar accesos y visibilidad de funcionalidades.
10. Estado de loading de un botón
    Tipo de estado: Local
    Ubicación: Componente (signal, variable, etc.)
    Justificación: Controla el spinner o el estado deshabilitado de un botón durante una operación específica.
11. Catálogo de productos
    Tipo de estado: Servidor
    Ubicación: TanStack Query (libs/services)
Justificación: Son datos del negocio que pueden reutilizarse desde caché en diferentes pantallas.
12. Organización activa (Multi-tenant)
    Tipo de estado: Global Compartido
    Ubicación: libs/state
    Justificación: Define el contexto global de la organización seleccionada y afecta las peticiones y datos de todas las aplicaciones.

**Explicar donde viviria cada uno: componente, libs/services, TanStack Query o libs/state.**


1. ¿El dato proviene de una base de datos externa a través de una API?
    ➡️ SÍ: Uso TanStack Query en `libs/services` para aprovechar la caché automática.
    ➡️ NO: (Ir al punto 2).

2. ¿La información es efímera, afecta únicamente a los elementos visuales de la pantalla actual o muere cuando el usuario navega a otra sección?
   ➡️ SÍ: Declaro un Estado Local (usando Angular Signals o variables de clase) directamente en el componente o feature.
   ➡️ NO: (Ir al punto 3).

3. ¿Múltiples aplicaciones independientes (`apps/`) o flujos transversales necesitan leer o modificar esta información en tiempo real sin recargar la página?
   ➡️ SÍ: Centralizo el estado en `libs/state` de forma global y estructurada.