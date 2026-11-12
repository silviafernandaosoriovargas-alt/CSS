# Catálogo de Maquillaje - Simulador CSS

Este repositorio contiene la solución correspondiente a la **Subactividad 1: Estructurar la jerarquía de estilos (Selectores, herencia, cascada y especificidad)**, desarrollada dentro del programa de formación **Análisis y Desarrollo de Software (ADSO)** (Ficha 3381732), bajo la tutoría del instructor John Freddy Becerra Castellanos.

## 1. Descripción del Proyecto

El objetivo de esta actividad es maquetar un catálogo web semántico enfocado en productos de maquillaje para aplicar y verificar de forma práctica las leyes fundamentales de CSS: herencia, cascada, especificidad y aislamiento por zonas mediante selectores combinados.

Siguiendo los lineamientos del instrumento de evaluación, el diseño se enfoca exclusivamente en la lógica de selección y colorimetría, omitiendo intencionalmente propiedades de modelo de caja, dimensiones o márgenes.

## 2. Estructura y Tecnologías Utilizadas

- **HTML5 Semántico:** Organización del documento mediante bloques semánticos principales (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>` y `<footer>`).
- **CSS3:** Implementación de herencia global, selectores combinados de descendientes y resolución de conflictos de especificidad.
- **Git & GitHub:** Control de versiones local y remoto gestionado mediante la rama `develop`.

## 3. Resumen del Cálculo de Puntos de Especificidad

Para determinar la autoridad de los selectores y resolver conflictos de estilo en el navegador, se utiliza el sistema matemático oficial de cálculo de especificidad:

| Tipo de Selector        | Identificador / Sintaxis | Puntuación de Especificidad | Ejemplos en el Proyecto          |
| ----------------------- | ------------------------ | --------------------------- | -------------------------------- |
| **Etiqueta (Elemento)** | `etiqueta`               | **1 pt**                    | `body`, `header`, `h2`, `p`, `a` |
| **Clase**               | `.clase`                 | **10 pts**                  | `.btn-comprar`, `.destacado`     |
| **Identificador**       | `#id`                    | **100 pts**                 | `#btn-destacado`                 |

### Demostración del Conflicto y Refactorización Final

1. **Conflicto de Autoridad (ID vs. Clase):** Inicialmente, al asignar a un elemento la clase `.btn-comprar` (10 pts) y el identificador `#btn-destacado` (100 pts), el peso del ID aplasta el orden lógico de la cascada, imponiendo su color sin importar cuál regla fue declarada primero en el código.
2. **Estandarización:** Posteriormente, se refactorizó la hoja de estilos eliminando las reglas basadas en `#id` y reemplazándolas por un sistema plano basado exclusivamente en clases combinadas (`.btn-comprar.destacado`), evitando de forma limpia la mala práctica de utilizar `!important`.

## 4. Conceptos Técnicos Aplicados

- **Herencia Global:** Declaración de la propiedad `font-family: sans-serif;` y del color de texto base en el selector `body`, permitiendo que los elementos hijos adopten estos estilos globalmente de forma heredada.
- **Aislamiento por Zonas (Selectores Combinados):** Uso de selectores específicos por ubicación para aplicar color a los enlaces sin interferir entre secciones:
  - `header nav ul li a`: Enlaces del menú de navegación principal.
  - `aside ul li a`: Enlaces del menú secundario de categorías.
  - `footer ul li a`: Enlaces de redes sociales y pie de página.

## 5. Control de Versiones

El avance técnico de la sesión se consolida en la nube ejecutando los siguientes comandos en la terminal local:

```bash
git add .
git commit -m "feat(ui): implementar modelo de caja y backgrounds"
git push origin feature/modelo-caja
## Hallazgos: El Modelo de Caja

1. **Diferencia práctica entre Margin y Padding:** El padding es el espacio de relleno interno entre el contenido y el borde de la caja, mientras que el margin es el espacio exterior que separa al elemento de otros elementos vecinos.
2. **Por qué es obligatorio usar `box-sizing: border-box`:** Evita que los bordes y rellenos sumen pixeles extras al ancho total, haciendo que las cajas mantengan las dimensiones programadas sin romper el diseño.
3. **Cómo se ven afectados los elementos hermanos:** Al aplicar un margen amplio a un elemento, este desplaza y aleja a los elementos contiguos para conservar su espacio de separación en la pantalla.

## Hallazgos: Centralización de Identidad Visual y Espaciado

En esta subactividad se implementó una "central de mando" usando el pseudoselector `:root` para organizar el diseño de nuestro catálogo de maquillaje. Estos son los hallazgos principales:

**(1) Lista completa de variables declaradas:**
*   **Colores:** Se definió la paleta corporativa basada en tonos rosados: `--color-primario` (#FF1493), `--color-secundario` (#FF69B4), `--color-terciario` (#FFA6C9), `--color-fondo-suave` (#FFD1DC), `--color-fondo-crema` (#fff8f9), `--color-texto` (#5c4b51) y `--color-blanco` (#ffffff).
*   **Tipografía:** Se vinculó la fuente de Google Fonts mediante la variable `--fuente-principal` ('Poppins', sans-serif).
*   **Espaciados (Box Model):** Se crearon medidas estandarizadas para no inventar valores: `--espaciado-pequeno` (8px), `--espaciado-medio` (16px), `--espaciado-grande` (24px) y `--espaciado-xl` (50px).

**(2) La ventaja de reutilizar medidas de margen y relleno:**
Antes de usar variables, asignar valores como "15px" o "20px" manualmente en cada selector era un riesgo. Si el cliente pedía cambiar la separación de las tarjetas, había que modificar el código línea por línea. Ahora, al usar `var(--espaciado-medio)`, garantizamos que todas las tarjetas tengan exactamente la misma proporción de aire. Si se necesita un cambio, se modifica solo una vez en el `:root` y se actualiza automáticamente en todo el sitio.

**(3) ¿Cómo previene colisiones visuales la centralización en :root?**
A medida que la hoja de estilos crece, es fácil equivocarse escribiendo un código hexadecimal a mano (por ejemplo, escribiendo un rosa ligeramente distinto). Al centralizar todo en `:root`, se elimina el error humano. Todos los elementos que usen `var(--color-primario)` serán idénticos. Esto previene que los diseños choquen entre sí, asegura una armonía visual perfecta y hace que el mantenimiento del código sea mucho más rápido y seguro a futuro.

## Hallazgos: Pseudoclases y Pseudoelementos

En esta subactividad "4" se añadió interactividad y decoración al catálogo usando CSS puro. Estos son los aprendizajes principales:

**(1) Diferencia funcional entre pseudoclase y pseudoelemento:**
Una **pseudoclase** (como `:hover` o `:focus`) se utiliza para definir el estado de un elemento existente; es decir, reacciona a una acción del usuario (como pasar el ratón o hacer clic). En cambio, un **pseudoelemento** (como `::before` o `::after`) se usa para inyectar contenido decorativo nuevo que no existe en el HTML, creando una caja virtual antes o después del elemento.

**(2) Importancia técnica del `:focus` para la accesibilidad:**
El uso de `:focus` es fundamental para la accesibilidad web (UX). No todos los usuarios navegan con un ratón; muchos lo hacen usando la tecla Tab del teclado. Al aplicar un contorno (`outline`) personalizado y visible en los enlaces del menú lateral, garantizamos que las personas con discapacidades visuales o motrices sepan exactamente en qué parte de la página están ubicados, cumpliendo con las normas de usabilidad.

**(3) Por qué inyectar decoración desde CSS (`::before/::after`) y no en HTML:**
Es una buena práctica mantener el HTML limpio y semántico. Si añadiéramos etiquetas `<span>` vacías solo para poner un punto en el menú o una etiqueta de "¡Oferta!" en los productos, ensuciaríamos el código y dificultaríamos su lectura. Al usar los pseudoelementos, el HTML solo se encarga de la estructura y el contenido, mientras que el CSS maneja toda la decoración visual de forma dinámica.

## Hallazgos: Arquitectura BEM y Modularidad

Durante el desarrollo de mi catálogo de maquillaje aprendí a organizar mejor los estilos de mi página utilizando la metodología BEM y separando el código CSS en diferentes archivos.

### 1. ¿Qué significa BEM y cómo se escribe?

BEM significa **Block, Element, Modifier** (Bloque, Elemento y Modificador).

Es una forma de organizar los nombres de las clases en HTML y CSS para identificar mejor cada parte de la página.

Se escribe de la siguiente manera:

- **Bloque:** es el componente principal. Ejemplo: `.tarjeta`.
- **Elemento:** es una parte que pertenece al bloque y se identifica con dos guiones bajos `__`. Ejemplo: `.tarjeta__titulo`.
- **Modificador:** sirve para darle una apariencia diferente a un componente y se identifica con dos guiones medios `--`. Ejemplo: `.tarjeta--destacada`.

Con esta metodología puedo identificar más fácilmente cada elemento y mantener el código organizado.

### 2. ¿Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo?

Dividir el CSS en varios archivos permite tener los estilos separados según su función. En mi proyecto creé archivos como `tarjetas.css`, `botones.css`, `menu-lateral.css` y `style.css`.

Esto facilita el trabajo en equipo porque cada persona puede trabajar en un componente diferente sin tener que modificar todo el código. También permite encontrar los estilos más rápido, hacer cambios y evitar tener toda la información en un solo archivo.

### 3. ¿Cómo evita la guerra de especificidad en CSS?

La guerra de especificidad ocurre cuando varios estilos intentan modificar el mismo elemento y algunos tienen más prioridad que otros, haciendo que sea difícil controlar cuál estilo se aplica.

Con BEM se utilizan clases más específicas y organizadas, evitando depender de selectores anidados demasiado largos.

Por ejemplo, en lugar de escribir `.producto h2`, utilizamos `.tarjeta__titulo`.

De esta manera, los estilos tienen una estructura más sencilla y un peso más plano, lo que ayuda a evitar conflictos entre las reglas CSS y facilita los cambios en el diseño.

### Conclusión

Con este ejercicio aprendí que organizar el código es importante para que un proyecto sea más fácil de entender, modificar y mantener. También comprendí que BEM y la modularidad ayudan a tener un código más ordenado y facilitan el trabajo cuando se desarrolla en equipo.
```
## Hallazgos: Arquitectura Total con Flexbox

**(1) ¿Por qué fue crucial aplicar `min-height: 100vh` y `flex-direction: column`?**
Para evitar que el pie de página (footer) quedara "flotando" en medio de la pantalla si había poco contenido. Al usar `column`, apilamos todo verticalmente, y con `100vh` obligamos a la página a medir lo mismo que la pantalla. Esto, junto con `flex: 1` en el centro, empuja el footer siempre hasta el fondo.

**(2) ¿Cómo la propiedad `gap` reemplazó los márgenes laterales?**
Antes usábamos `margin-right` en cada enlace, lo que ensuciaba el código y dejaba un espacio extra al final de la lista. Con `gap`, el contenedor padre calcula automáticamente una separación exacta y uniforme entre todos sus elementos hijos, haciendo el código más limpio.

**(3) ¿Cómo BEM, Variables y Flexbox crearon tarjetas resistentes?**
BEM nos dio clases claras (ej. `.tarjeta__descripcion`), las Variables mantuvieron los colores unificados, y Flexbox (con `flex-grow: 1` en la descripción) creó un "resorte invisible". Si un texto es corto y otro largo, este resorte se estira para empujar el botón de compra siempre al fondo, logrando que todas las tarjetas midan igual y los botones queden alineados.