# Plantilla de apuntes (LaTeX)

Plantilla LaTeX para escribir **apuntes de asignatura**, basada en la
[Plantilla de documento corto](https://github.com/alfco28/Plantilla_doc_corto)
pero más informal y adaptada a apuntes. Cada asignatura es un proyecto
independiente que usa esta plantilla como base.

## Compilación

- **Compilar con XeLaTeX** (en Overleaf: *Menu → Compiler → XeLaTeX*).
- Dos pasadas para que el índice y las referencias cruzadas se estabilicen.
- Fuentes necesarias: *Latin Modern Roman* (texto) y *Fira Mono* (código),
  ambas disponibles en Overleaf de serie.

## Estructura

```
main.tex                  Preámbulo completo + estructura del documento
front_matter/
  title_page.tex          Portada
main_matter/
  tema_1.tex              Tema 1 (contenido de ejemplo)
  tema_2.tex              Tema 2 (contenido de ejemplo: TikZ, tablas, algoritmos…)
```

## Uso

- **Cada tema es una sección**: los temas entran con `\input{main_matter/tema_N}`
  en `main.tex` (o simplemente escribe los temas directamente en un solo
  archivo, la plantilla no impone nada). El título y el índice muestran
  «Tema 1», «Tema 2», … automáticamente a partir del número de sección; la
  numeración interna (Teorema 1.1, Definición 1.2, …) no cambia.
- **Sin front/back matter**: solo portada e índice (numerados en romano);
  el resto, numeración arábiga desde 1.
- **Portada**: edita las variables `\universidad`, `\title`, `\author`,
  `\fecha` en `main.tex`.

## Puntos configurables (todos en `main.tex`)

| Comando             | Por defecto      | Qué controla                                                  |
|---------------------|------------------|---------------------------------------------------------------|
| `\interlineado`     | `1.2`            | Interlineado de todo el documento (afecta a todos los tamaños de letra). |
| `\sangriaentorno`   | `1.5em`          | Sangría francesa de los entornos (líneas 2.ª y siguientes).  |
| `\reservaminima`    | `5\baselineskip` | Espacio mínimo que se reserva al empezar un entorno, para que un teorema y su demostración no queden separados por un salto de página. |

## Entornos

Todos los entornos admiten la nota opcional `\begin{teorema}[Nombre]`,
se numeran por sección y se referencian con `\cref` (con nombre en
castellano: «teorema 1.1», «definición 1.2», …):

`teorema`, `lema`, `proposicion`, `corolario`, `propiedad`, `axioma`,
`criterio` (comparten el contador del teorema), `definicion`, `ejemplo`,
`observacion`, `nota`, `conjetura`, `problema`, `notacion` (cada uno con
su contador) y `demostracion` (sin numerar, con `\qed` automático).

Las **demostraciones** se escriben con `\begin{demostracion} …
\end{demostracion}` (o `\begin{demostracion}[Nombre]`) y quedan siempre
pegadas a su resultado: la plantilla evita que salte una página entre un
enunciado y su demostración, y aplica también la sangría francesa.

## Recomendaciones

- Usa `\cref` / `\Cref` (cleveref) para todas las referencias cruzadas:
  los nombres ya están en castellano.
- Las notas al margen (`\marginpar` o `marginnote`) sirven para
  mini-índices de términos y referencias cruzadas, como en el Diestel.
- Pensada para imprimirse en A4 y en blanco y negro: evita colores salvo
  que aporten algo pedagógico.
