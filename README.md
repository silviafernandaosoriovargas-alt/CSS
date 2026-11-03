# Catálogo de Maquillaje - Simulador CSS

Este repositorio contiene la solución correspondiente a la **Subactividad 1: Estructurar la jerarquía de estilos (Selectores, herencia, cascada y especificidad)**, desarrollada dentro del programa de formación **Análisis y Desarrollo de Software (ADSO)** (Ficha 3234206), bajo la tutoría del instructor John Freddy Becerra Castellanos.

## 1. Descripción del Proyecto

El objetivo de esta actividad es maquetar un catálogo web semántico enfocado en productos de maquillaje para aplicar y verificar de forma práctica las leyes fundamentales de CSS: herencia, cascada, especificidad y aislamiento por zonas mediante selectores combinados.

Siguiendo los lineamientos del instrumento de evaluación, el diseño se enfoca exclusivamente en la lógica de selección y colorimetría, omitiendo intencionalmente propiedades de modelo de caja, dimensiones o márgenes.

## 2. Estructura y Tecnologías Utilizadas

* **HTML5 Semántico:** Organización del documento mediante bloques semánticos principales (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>` y `<footer>`).
* **CSS3:** Implementación de herencia global, selectores combinados de descendientes y resolución de conflictos de especificidad.
* **Git & GitHub:** Control de versiones local y remoto gestionado mediante la rama `develop`.

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

* **Herencia Global:** Declaración de la propiedad `font-family: sans-serif;` y del color de texto base en el selector `body`, permitiendo que los elementos hijos adopten estos estilos globalmente de forma heredada.
* **Aislamiento por Zonas (Selectores Combinados):** Uso de selectores específicos por ubicación para aplicar color a los enlaces sin interferir entre secciones:
  * `header nav ul li a`: Enlaces del menú de navegación principal.
  * `aside ul li a`: Enlaces del menú secundario de categorías.
  * `footer ul li a`: Enlaces de redes sociales y pie de página.

## 5. Control de Versiones

El avance técnico de la sesión se consolida en la nube ejecutando los siguientes comandos en la terminal local:

```bash
git add .
git commit -m "feat(styles): maquetar catalogo semantico y aplicar jerarquia CSS"
git push origin develop