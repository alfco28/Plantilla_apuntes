# Plantilla de apuntes (LaTeX)

Plantilla LaTeX para escribir **apuntes de asignatura**, basada en la
[Plantilla de documento corto](https://github.com/alfco28/Plantilla_doc_corto)
pero más informal y adaptada a apuntes. Cada asignatura es un proyecto
independiente que usa esta plantilla como base.

## Compilación

- **Compilar con XeLaTeX** (en Overleaf: *Menu → Compiler → XeLaTeX*).
- Dos pasadas para que el índice y las referencias cruzadas se estabilicen.
- Fuentes necesarias: *Fira Sans* (texto), *Fira Math* (fórmulas) y *Fira Mono*
  (código), todas ellas sin serifa y a juego, disponibles en Overleaf de serie.

## Estructura

```
main.tex                  Preámbulo completo + estructura del documento
front_matter/
  title_page.tex          Portada
main_matter/
  tema_1.tex              Tema 1 (contenido de ejemplo)
  tema_2.tex              Tema 2 (contenido de ejemplo: TikZ, tablas, algoritmos…)
```

Los ficheros pueden estar en esas carpetas **o directamente sueltos en la
raíz del proyecto**: `main.tex` los busca en su carpeta y, si no están
ahí, los busca en la raíz, de modo que ambas disposiciones funcionan.

## Uso

- **Cada tema es una sección**: los temas entran con `\inputtema{tema_N}`
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
| `\sangriaentorno`   | `2em`            | Sangría francesa de los entornos (líneas 2.ª y siguientes).  |
| `\reservaminima`    | `5\baselineskip` | Espacio mínimo que se reserva al empezar un entorno, para que un teorema y su demostración no queden separados por un salto de página. |

## Entornos

Todos los entornos admiten la nota opcional `\begin{teorema}[Nombre]`,
se numeran por sección y se referencian con `\cref`:

`teorema`, `lema`, `corolario`, `propiedad`, `axioma`,
`criterio` (comparten el contador del teorema), `definicion`, `ejemplo`,
`observacion`, `nota`, `conjetura`, `problema`, `notacion` (cada uno con
su contador) y `demostracion` (sin numerar, con `\qed` automático).

Los **encabezados van abreviados como en mis apuntes a mano**: «Def.: 1.1»,
«Ej.: 1.2», «Obs.: 1.3», «Prop.: 1.4» y «Dem.:» para las demostraciones;
los nombres cortos o principales van completos: «Teorema 1.1», «Lema 1.2»,
«Nota», «Notación», «Criterio», «Problema». `cleveref` usa el mismo
sistema: «def. 1.1» y, en plural, «def.s 1.1 y 1.2».

Las **demostraciones** se escriben con `\begin{demostracion} …
\end{demostracion}` (o `\begin{demostracion}[Nombre]`) y quedan siempre
pegadas a su resultado: la plantilla evita que salte una página entre un
enunciado y su demostración, y aplica también la sangría francesa.

## Cómo redactar los apuntes (mi estilo a mano)

Los apuntes se redactan **en mi estilo manuscrito**: telegráfico y compacto,
con mis abreviaturas literales dentro del cuerpo (no expandidas). Resumen del
sistema (la versión completa y actualizada vive en mi base de conocimiento):

**Abreviaturas y su plural.** Abreviatura con punto y plural añadiendo `s`
tras el punto: `aplic.` → `aplic.s`, `var. dif.` → `var.s dif.s`. Abreviaturas
habitual: `aplic.` (aplicación), `cont.`, `dif.`, `esp.`, `e.t.` (espacio
topológico), `v.d.` (variedad diferenciable), `conj.`/`subconj.`, `top.`
(topología; `top. induc.` = inducida), `dim.`, `func. obj.`, `resp.`,
`t.q.` (tal que), `i.e.`, `sup.` (supongamos), `s.a.` (sujeto a) y `c.c.`
(caso contrario). El símbolo `#` significa «número de»: «# de pasos»,
«# finito de elementos». Las siglas se definen entre paréntesis en su
primer uso (`OC`, `e.t.`, …) y el término inglés se anota también entre
paréntesis: «(TSP) Travel Salesman Problem».

**Estructura de un tema.** Primero la intuición en palabras cortas entre
comillas, a menudo con una figura (TikZ), y luego Def. → Ej. → Obs. →
propiedades y Teoremas con su `demostracion` pegada. Los enunciados pueden
empezar con la versión informal entre comillas y a continuación la
formalización: `Prop.: "la composición de aplic.s dif.s también es dif.",
Sean… Se tiene que…`.

**Demostraciones.** Conectivas mías: «Veamos que», «Sup. que», «Luego»,
«ya que», «basta con», «por las reglas del cálculo», «Análogo al
anterior», «Recordamos», «Comprobemos que funciona»; casos con guiones
(`- A abierto:` … `- A cerrado:`) o por direcciones (`⇒` / `⇐` en bloques);
`\underbrace` con la justificación de cada factor («Dif. por comp. de
cartas»); anclas numeradas ①②③ para razonar luego sobre subexpresiones
(«Luego ① y ③ no alteran el rango ⇒ r = r'»), y en cadena larga, la
conclusión en palabras.

**Modelización (programación).** Estructura fija: **Inputs** → **Var.s**
(cada binaria por casos: `x_j = {1 si …, 0 c.c.}`) → **Func. obj.**
(`min`/`max`) → **Restricciones** (`s.a.`), y **cada restricción con su
comentario explicativo entre paréntesis** a la derecha: `Σ a_ij x_j ≥ 1, ∀i
(Todos los clientes cubiertos)`. Los algoritmos se iteran a mano en los
apuntes (`Iter 1. Restric. 1: …`) con la decisión al margen y el criterio
de parada escrito en palabras.

**Márgenes.** Con `\notamargen{}`: aclaraciones de figuras («proy.
estereográfica desde el polo norte»), avisos («No confundir con…»),
vértices «Sí/No actualizamos», y las preguntas pendientes («Esto no está
bien del todo, ¿por qué? Preguntar al prof.»).

## Recomendaciones

- Usa `\cref` / `\Cref` (cleveref) para todas las referencias cruzadas:
  los nombres ya siguen el sistema de abreviaturas (teorema, def., ej.).
- Las notas al margen (`\marginpar` o `marginnote`) sirven para
  mini-índices de términos y referencias cruzadas, como en el Diestel.
- Los símbolos matemáticos los aporta *Fira Math* a través de
  `unicode-math` (por eso la plantilla no carga `amssymb`); `\mathbb`,
  `\mathcal`, etc. funcionan igual.
- Pensada para imprimirse en A4 y en blanco y negro: evita colores salvo
  que aporten algo pedagógico.
