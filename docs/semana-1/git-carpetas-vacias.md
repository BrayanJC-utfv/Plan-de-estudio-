Respuestas dudas semana 1 - Git y Carpetas Vacías

--¿Por qué Git no detecta carpetas vacías?--

Git realiza seguimiento únicamente de archivos. Si una carpeta está vacía, Git la ignora y no la incluirá en los commits.

Ejemplo:

apps/
└── shell/

La carpeta `shell` no aparecerá en `git status` mientras no contenga archivos.

--¿Qué es .gitkeep?--

`.gitkeep` es un archivo vacío utilizado por convención para obligar a Git a conservar una carpeta que aún no contiene archivos reales.

Ejemplo:

apps/
└── shell/
    └── .gitkeep

De esta forma, Git puede versionar la carpeta.

--¿Qué es .gitignore?--

`.gitignore` es un archivo que indica a Git qué archivos o carpetas no deben incluirse en el control de versiones.

--Conclusión--

Las carpetas vacías no son rastreadas por Git. El archivo `.gitkeep` permite conservar la estructura de directorios del proyecto, mientras que `.gitignore` evita que archivos innecesarios sean versionados.