# Testimonios · Práctica inicial de React

Aplicación que muestra testimonios ficticios de uno en uno, con navegación
manual (Anterior, Siguiente, Aleatorio) y reproducción automática, construida con React y Vite.

## Integrantes
- Martínez Flores Javier Alexander
- Hernández López Clara Paulina

## Enlaces
- Repositorio: https://github.com/LilTacoH2O/React_Testimonios
- Tablero Scrum: https://github.com/users/LilTacoH2O/projects/1
- Sitio publicado: https://testimonios-javier-clara.surge.sh/

## Etapa actual
Etapa básica (P01–P10) y ampliación con reproducción automática (A01–A07) terminadas.
Experimento de reutilización realizado.

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
- `src/App.jsx`: componente principal; conserva el índice y la reproducción con `useState`, y el temporizador con `useEffect`.
- `src/data.js`: arreglo de ocho testimonios ficticios (tres del docente y cinco agregados).
- `src/components/Testimonial.jsx`: presenta un testimonio recibido por props.
- `src/components/Controls.jsx`: botones Anterior, Siguiente y Aleatorio que avisan a App con callbacks.
- `src/styles.css`: estilos responsive (320, 768 y 1280 px), foco visible y botones de 44 px.

## Decisiones principales
1. **Datos separados de la presentación.** `data.js` solo contiene datos;
   `Testimonial` no importa `data.js`, recibe el objeto por la prop `item`.
2. **Componente reutilizable.** `Testimonial` presenta cualquier testimonio;
   no elige personas ni modifica el arreglo.
3. **Estilos propios.** Se quitaron `App.css`, `index.css` y `src/assets` de la plantilla de Vite;
   los estilos se importan una sola vez desde `main.jsx`.
4. **Un solo dueño del estado.** Solo `App` guarda el índice (`useState`).
   `Controls` no cambia el índice: recibe `onPrev`, `onNext` y `onRandom` y avisa con el clic.
5. **Navegación circular.** Se usa `%` para pasar del último al primero; en `prev`
   se suma `total` para evitar un índice negativo.
6. **Aleatorio sin repetir.** Se elige un salto entre 1 y `total - 1`, así nunca
   muestra el mismo testimonio cuando hay dos o más.
7. **Casos de 0 y 1 registros.** Con 0 se muestra un mensaje sin acceder a los campos;
   con 1, `random` no hace nada y los demás botones mantienen el registro.
8. **Diseño adaptable y accesible.** La tarjeta mide como máximo 560 px y ocupa todo el ancho en móvil;
   `overflow-wrap: anywhere` evita el desplazamiento horizontal con textos largos;
   los botones miden al menos 44 px y tienen foco visible para usarse con teclado.
9. **Temporizador en un efecto.** La reproducción automática usa `useEffect` con limpieza
   (`clearInterval`) y dependencias `[reproduciendo, total]`; la navegación manual la pausa.

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
| 04 | #5 | `Controls` y navegación con `useState` (Anterior, Siguiente, Aleatorio) | Clara | Javier | #15 |
| 05 | #6 | Estilos responsive y foco visible | Javier | Clara | #17 |
| 06 | #7 | Ocho registros y pruebas P01–P10 | Clara | Javier | #18 |
| 07 | #8 | Revisión por otra pareja; se atendieron sus sugerencias | Javier | Clara | #19 |
| 08 | #9 | Reproducción automática con `useEffect` (Pausar/Reanudar) | Javier | Clara | #__ |
| 09 | #10 | Experimento de reutilización (rama `experimento-reutilizacion`) | Clara | Javier | este PR |

## Traza del índice (tres registros)

| Acción | Índice antes | Cálculo | Índice después | Pantalla |
|---|---|---|---|---|
| Inicio | — | `useState(0)` | 0 | Ana Pérez · 1 de 3 |
| Siguiente | 0 | `(0 + 1) % 3` | 1 | Luis García · 2 de 3 |
| Siguiente | 1 | `(1 + 1) % 3` | 2 | María López · 3 de 3 |
| Siguiente | 2 | `(2 + 1) % 3` | 0 | Ana Pérez · 1 de 3 |
| Anterior | 0 | `(0 - 1 + 3) % 3` | 2 | María López · 3 de 3 |

## Pruebas de la etapa básica (P01–P10)
P01 a P07 se hicieron con los tres registros iniciales; P06 y P07 se hicieron
comentando temporalmente los objetos de `data.js`, que después se restauró.

| Prueba | Acción y resultado esperado | Resultado obtenido | Estado |
|---|---|---|---|
| P01 Inicio | Se muestra Ana y la posición 1 de 3 | Ana Pérez · Testimonio 1 de 3 | Aprobado |
| P02 Siguiente | Desde Ana, Siguiente muestra Luis y 2 de 3 | Luis García · 2 de 3 | Aprobado |
| P03 Límite superior | Desde María, Siguiente muestra Ana | Regresa a Ana · 1 de 3 | Aprobado |
| P04 Límite inferior | Desde Ana, Anterior muestra María | María López · 3 de 3 | Aprobado |
| P05 Aleatorio | Cambia a otro válido (10 veces) | Nunca repitió el actual; la lógica usa un salto de 1 a total − 1 | Aprobado |
| P06 Un registro | Con un objeto, los controles mantienen el registro | Se queda Ana · 1 de 1, sin errores | Aprobado |
| P07 Sin registros | Con [] aparece el mensaje y no hay controles | "No hay testimonios disponibles." sin botones | Aprobado |
| P08 Ocho registros | Navegación completa y contador de 8 | Recorre los 8 y vuelve a 1 de 8 | Aprobado |
| P09 Presentación | Tres anchos, texto largo y teclado | Sin scroll horizontal en 320, 768 y 1280 px; texto largo ajustado; foco visible con Tab | Aprobado |
| P10 Compilación | npm run build sin errores | Build correcto; consola sin errores de la aplicación | Aprobado |

### Corrección registrada
- **Entrada:** en el Avance 2 se hizo el commit sin crear antes la rama `avance-02-datos`.
- **Resultado observado:** el commit quedó en `main` y `git push -u origin avance-02-datos`
  falló con "src refspec avance-02-datos does not match any".
- **Resultado esperado:** el commit debía subirse en su propia rama para revisarse con un Pull Request.
- **Corrección:** se creó la rama con `git switch -c avance-02-datos`, se regresó `main`
  con `git branch -f main origin/main` y se volvió a hacer el push. Se comprobó en GitHub
  que la rama tenía el commit y que `main` no había cambiado.

### Revisión de consola
Los errores que aparecían en la consola de Chrome venían de una extensión del navegador
y de la simulación de red sin conexión de las herramientas de desarrollo (Network throttling en Offline).
Con la red normal y en una ventana de incógnito, la consola no mostró errores de la aplicación.

## Revisión por otra pareja
- **Pareja revisora:** Juan Martín Arriaga Alejos y Owen Alberto Hernández Naranjillo.
- **Medio:** la revisión se recibió en nuestro Google Doc; captura en el documento de evidencias
  y transcripción en el issue #8.
- **Qué revisaron:** repositorio, tablero y sitio publicado. Confirmaron que Testimonial solo presenta,
  Controls solo avisa con callbacks, App es el único que guarda el índice, los extremos y Aleatorio
  funcionan, se manejan 0 y 1 registros, se ve bien en móvil y con teclado, y P01–P10 tienen resultados.
- **Sugerencias recibidas:**
  1. Agregar el enlace real del tablero en el README.
  2. Quitar la carpeta `src/assets`, que ya no se usaba.
- **Cambios realizados:** se agregó el enlace del tablero (y el del sitio publicado) y se eliminó `src/assets`.
- **Revisión que hicimos nosotros:** revisamos el proyecto de la misma pareja
  (https://github.com/nitram047/carousel-testimonial).

## Ampliación: reproducción automática (A01–A07)
- **Funcionamiento:** el carrusel empieza pausado. Reanudar avanza cada 5 segundos; Pausar lo detiene;
  usar Anterior, Siguiente o Aleatorio pausa la reproducción.
- **useEffect:** el temporizador es externo al cálculo del JSX, por eso se crea en un efecto y no en el cuerpo de App.
  Solo se crea si `reproduciendo` es verdadero y hay al menos dos registros.
- **Limpieza:** `return () => clearInterval(intervalo)` elimina el intervalo antes de repetir el efecto
  y al desmontar el componente; evita intervalos acumulados.
- **Dependencias:** `[reproduciendo, total]`; el efecto se sincroniza otra vez solo si cambian.
- Se quitó `aria-live` del contador para no anunciar la posición cada 5 segundos.

| Prueba | Resultado esperado | Resultado obtenido | Estado |
|---|---|---|---|
| A01 Activación | Reanudar inicia avances cada ~5 s | Avanza cada ~5 s y el botón cambia a Pausar | Aprobado |
| A02 Pausa | Pausar mantiene el testimonio | Se queda fijo más de 5 s | Aprobado |
| A03 Acción manual | Anterior/Siguiente/Aleatorio cambian y pausan | Cambia y el botón vuelve a Reanudar | Aprobado |
| A04 Reanudación | Varias veces sin aceleración | Mantiene ~5 s entre cambios | Aprobado |
| A05 Límites | El último vuelve al primero | Del 8 pasa al 1 | Aprobado |
| A06 Pocos datos | Con 0 o 1 registro no se crea un intervalo | Con 1 registro no aparece Reanudar; con 0 aparece el mensaje sin botones | Aprobado |
| A07 Limpieza | Sin intervalos acumulados | Tras alternar Pausar/Reanudar sigue cada ~5 s; al pausar se detiene; `clearInterval` en el return del efecto | Aprobado |

## Experimento de reutilización
Se hizo en la rama `experimento-reutilizacion`, que no se fusionó a `main`.
- **Qué se hizo:** se mostraron dos tarjetas más con el mismo componente
  (`<Testimonial item={testimonios[0]} />` y `<Testimonial item={testimonios[1]} />`)
  y se cambió una sola regla de `.testimonial-card` (el color de fondo a `#fff8e1`).
- **Resultado:** las tres tarjetas recibieron el cambio al mismo tiempo, porque todas usan `Testimonial`.
- **Duplicación evitada:** sin el componente habría que copiar la imagen, el nombre, el cargo y el
  comentario en cada lugar, y repetir cada cambio visual en todas las copias.

| Cambio solicitado | Lugar principal del cambio |
|---|---|
| Agregar un testimonio | `data.js` |
| Modificar la tarjeta de todas las personas | `Testimonial.jsx` y sus estilos |
| Cambiar los textos de los controles | `Controls.jsx` |
| Cambiar el comportamiento de navegación | `App.jsx` |
| Modificar apariencia sin cambiar navegación | `styles.css` |