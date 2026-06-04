Dia 5: cierre de semana y estandar de trabjo

Indice de documentacion semana 1
1.Resumir rquitectura, roles de carpetas y mitigacion de riesgos - docs/semana-1/arquitectura.md
2.Agregar casos de uso y recomnedaciones prara http y jwt - docs/semana-1/http-status-notas.md
3.Agregar casos de uso y recomnedaciones prara http y jwt - docs/semana-1jwt-notas.md
4.Estado del servidor con TanStack Query - docs/semana-1/tanstack-query-notas.md
5.Estilos con Tailwind CSS v3 - docs/semana-1/tailwind-v3-notas.md
6.Diseño conceptual de card Responsive - docs/semana-1/pagina-practica.md
7.Resumen y dudas de cierre - docs/semana-1/resumen-final.md 

--Flujo de Trabajo Recomendado (Estándar del Equipo)--

1.Crear Rama Teatral: Nunca trabajar directo en ramas principales; usar feature/nombre-tarea.
2.Setup Local Inicial: Ejecutar pnpm install --frozen-lockfile y pnpm run prepare:dev para evitar errores de arranque.
3.Validación de Puertos: Correr pnpm run preflight:ports antes de levantar entornos para evitar colisiones.
4.Desarrollo Limpio: Escribir código respetando las reglas de fronteras de imports.
5.Verificación Obligatoria: Antes de abrir un Pull Request (PR), ejecutar los scripts de verificación local:
   pnpm run verify:workspace
   pnpm run verify:test-presence
   pnpm run verify:component-complexity
6.Commits Profesionales: Guardar cambios estructurados bajo la especificación de Conventional Commits.