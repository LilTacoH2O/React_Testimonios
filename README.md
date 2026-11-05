# Testimonios · Práctica inicial de React

Aplicación que muestra testimonios ficticios de uno en uno, con navegación
manual (Anterior, Siguiente, Aleatorio), construida con React y Vite.

## Integrantes
- Martínez Flores Javier Alexander
- Hernández López Clara Paulina

## Enlaces
- Repositorio: https://github.com/LilTacoH2O/React_Testimonios
- Tablero Scrum: [pegar enlace del proyecto React Testimonios · Scrum]

## Etapa actual
En desarrollo: Sprint 1 · Etapa básica.

## Versiones
- Node.js: v24.15.0
- npm: 11.12.1
- Vite: 8.3.5 · React: 19 (ver package.json)

## Instalación y ejecución
```bash
npm install
npm run dev       # desarrollo
npm run build     # versión de producción en dist/
npm run preview   # revisar la compilación localmente
```

## Estructura
- `index.html`: contiene `<div id="root">` y carga `src/main.jsx`.
- `src/main.jsx`: crea la raíz de React, importa los estilos y monta App.
- `src/App.jsx`: componente principal; elige el testimonio que se muestra.
- `src/data.js`: arreglo de testimonios ficticios (datos del docente).
- `src/components/Testimonial.jsx`: presenta un testimonio recibido por props.
- `src/styles.css`: estilos de la práctica (se completan en el avance 5).

## Decisiones principales
1. **Datos separados de la presentación.** `data.js` solo contiene datos;
   `Testimonial` no importa `data.js`, recibe el objeto por la prop `item`.
2. **Componente reutilizable.** `Testimonial` presenta cualquier testimonio;
   no elige personas ni modifica el arreglo.
3. **Estilos propios.** Se quitaron `App.css` e `index.css` de la plantilla de Vite;
   los estilos se importan una sola vez desde `main.jsx`.

## Scrum y Pair Programming
Historia de usuario: "Como visitante de un sitio web, quiero consultar testimonios
de clientes mediante controles de navegación para conocer sus experiencias con el servicio."

Tablero con columnas Pendiente, En proceso, En revisión y Terminado.
Sprint 1 · Etapa básica (19 puntos) y Sprint 2 · Ampliación (9 puntos).
En cada avance se alternan los roles de Driver (conductor) y Navigator (observador);
el Driver hace el commit y abre el Pull Request, y el Navigator lo revisa y lo fusiona.

## Registro de avances

| Avance | Issue | Qué se hizo | Driver | Navigator | PR |
|---|---|---|---|---|---|
| 01 | #2 | Proyecto base con Vite + React | Javier | Clara | commit directo a main |
| 02 | #3 | `data.js` con los tres testimonios del docente | Clara | Javier | #12 |
| 03 | #4 | Componente `Testimonial` y montaje con `main.jsx` | Javier | Clara | #13 |