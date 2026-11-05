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
- `src/App.jsx`: componente principal; conserva el índice con `useState` y coordina la navegación.
- `src/data.js`: arreglo de testimonios ficticios (datos del docente).
- `src/components/Testimonial.jsx`: presenta un testimonio recibido por props.
- `src/components/Controls.jsx`: botones Anterior, Siguiente y Aleatorio que avisan a App con callbacks.
- `src/styles.css`: estilos de la práctica (se completan en el avance 5).

## Decisiones principales
1. **Datos separados de la presentación.** `data.js` solo contiene datos;
   `Testimonial` no importa `data.js`, recibe el objeto por la prop `item`.
2. **Componente reutilizable.** `Testimonial` presenta cualquier testimonio;
   no elige personas ni modifica el arreglo.
3. **Estilos propios.** Se quitaron `App.css` e `index.css` de la plantilla de Vite;
   los estilos se importan una sola vez desde `main.jsx`.
4. **Un solo dueño del estado.** Solo `App` guarda el índice (`useState`).
   `Controls` no cambia el índice: recibe `onPrev`, `onNext` y `onRandom` y avisa con el clic.
5. **Navegación circular.** Se usa `%` para pasar del último al primero; en `prev`
   se suma `total` para evitar un índice negativo.
6. **Aleatorio sin repetir.** Se elige un salto entre 1 y `total - 1`, así nunca
   muestra el mismo testimonio cuando hay dos o más.
7. **Casos de 0 y 1 registros.** Con 0 se muestra un mensaje sin acceder a los campos;
   con 1, `random` no hace nada y los demás botones mantienen el registro.

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
| — | — | README con estructura, decisiones y registro de avances | Javier | Clara | #14 |
| 04 | #5 | `Controls` y navegación con `useState` (Anterior, Siguiente, Aleatorio) | Clara | Javier | #__ |

## Traza del índice (tres registros)

| Acción | Índice antes | Cálculo | Índice después | Pantalla |
|---|---|---|---|---|
| Inicio | — | `useState(0)` | 0 | Ana Pérez · 1 de 3 |
| Siguiente | 0 | `(0 + 1) % 3` | 1 | Luis García · 2 de 3 |
| Siguiente | 1 | `(1 + 1) % 3` | 2 | María López · 3 de 3 |
| Siguiente | 2 | `(2 + 1) % 3` | 0 | Ana Pérez · 1 de 3 |
| Anterior | 0 | `(0 - 1 + 3) % 3` | 2 | María López · 3 de 3 |