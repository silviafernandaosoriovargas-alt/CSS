# Catálogo de Maquillaje - Simulador CSS

Este repositorio contiene la solución correspondiente a la **Subactividad 1: Estructurar la jerarquía de estilos (Selectores, herencia, cascada y especificidad)**, desarrollada dentro del programa de formación **Análisis y Desarrollo de Software (ADSO)** (Ficha 3234206), bajo la tutoría del instructor John Freddy Becerra Castellanos.

## 1. Descripción del Proyecto

El objetivo de esta actividad es maquetar un catálogo web semántico enfocado en productos de maquillaje para aplicar y verificar de forma práctica las leyes fundamentales de CSS: herencia, cascada, especificidad y aislamiento por zonas mediante selectores combinados.

Siguiendo los lineamientos del instrumento de evaluación, el diseño se enfoca exclusivamente en la lógica de selección y colorimetría, omitiendo intencionalmente propiedades de modelo de caja, dimensiones o márgenes.

## 2. Estructura y Tecnologías Utilizadas

- **HTML5 Semántico:** Organización del documento mediante bloques semánticos principales (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>` y `<footer>`).
- **CSS3:** Implementación de herencia global, selectores combinados de descendientes y resolución de conflictos de especificidad.
- **Git & GitHub:** Control de versiones local y remoto gestionado mediante la rama `develop`.

## 3. Resumen del Cálculo de Puntos de Especificidad

Para determinar la autoridad de los selectores y resolver conflictos de estilo en el navegador, se utiliza el sistema matemático oficial de cálculo de especificidad:

| Tipo de Selector | Identificador / Sintaxis | Puntuación de Especificidad | Ejemplos en el Proyecto |
| --- | --- | --- | --- |
| **Etiqueta (Elemento)** | `etiqueta` | **1 pt** | `body`, `header`, `h2`, `p`, `a` |
| **Clase** | `.clase` | **10 pts** | `.btn-comprar`, `.destacado` |
| **Identificador** | `#id` | **100 pts** | `#btn-destacado` |

### Demostración del Conflicto y Refactorización Final

1. **Conflicto de Autoridad (ID vs. Clase):** Inicialmente, al asignar a un elemento la clase `.btn-comprar` (10 pts) y el identificador `#btn-destacado` (100 pts), el peso del ID aplasta el orden lógico de la cascada, imponiendo su color sin importar cuál regla fue declarada primero en el código.
2. **Estandarización:** Posteriormente, se refactorizó la hoja de estilos eliminando las reglas basadas en `#id` y reemplazándolas por un sistema plano basado exclusivamente en clases combinadas (`.btn-comprar.destacado`), evitando de forma limpia la mala práctica de utilizar `!important`.

## 4. Conceptos Técnicos Aplicados

- **Herencia Global:** Declaración de la propiedad `font-family: sans-serif;` y del color de texto base en el selector `body`, permitiendo que los elementos hijos adopten estos estilos globalmente de forma heredada.
- **Aislamiento por Zonas (Selectores Combinados):** Uso de selectores específicos por ubicación para aplicar color a los enlaces sin interferir entre secciones:
  * `header nav ul li a`: Enlaces del menú de navegación principal.
  * `aside ul li a`: Enlaces del menú secundario de categorías.
  * `footer ul li a`: Enlaces de redes sociales y pie de página.

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