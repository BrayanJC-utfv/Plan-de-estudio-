Dia 4:  Notas de TanStack Query (Estado del Servidor)

--Notas de Tailwind CSS v3 (Estilos Utilitarios)--

Tailwind CSS es un framework que permite diseñar interfaces directo en las clases del HTML/Angular utilizando clases utilitarias de bajo nivel.

Utilidades Base y Ejemplos
Layout / Flexbox: flex, flex-col, items-center, justify-between -> Controlan la alineación de cajas.
Espaciados: p-4 (padding general), mx-2 (margen horizontal), space-y-4 (separación vertical uniforme entre hijos).
Tipografía: text-lg (tamaño de fuente), font-bold (grosor), text-slate-800 (color del texto).
Estados / Interactividad:** hover:bg-blue-600 (cambio de color al pasar el cursor), focus:ring (borde de enfoque en inputs).

--Caso Real en el Frontend y Acción Recomendada--
Caso: Te piden que crees un botón de acción en la app workspace que al pasar el mouse encima cambie sutilmente de color y que en pantallas de celulares ocupe todo el ancho pero en computadoras sea pequeño.Acción Recomendada: Utiliza las clases de diseño responsivo y pseudo-clases de Tailwind: `<button class="w-full md:w-auto bg-blue-500 hover:bg-blue-600 text-white p-2 rounded">`. El prefijo `md: asegura el comportamiento adaptativo sin escribir una sola línea de CSS tradicional.