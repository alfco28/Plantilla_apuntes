# Plantilla de apuntes (LaTeX)

Plantilla LaTeX para escribir **apuntes de asignatura**, basada en la
[Plantilla de documento corto](https://github.com/alfco28/Plantilla_doc_corto)
pero más informal y adaptada a apuntes. Cada asignatura es un proyecto
independiente que usa esta plantilla como base.

## Compilación

- **Compilar con XeLaTeX** (en Overleaf: *Menu → Compiler → XeLaTeX*).
- Dos pasadas para que el índice y las referencias cruzadas se estabilicen.
- Fuentes necesarias: *Fira Sans* (texto), *Fira Math* (fórmulas) y *Fira Mono*
  (código), todas ellas sin serifa y a juego, disponibles en Overleaf de serie;
  más *Latin Modern Math*, también de serie, de la que la plantilla toma
  solo algunos símbolos que faltan en Fira Math (véanse los
  «Detalles técnicos»).

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
- **Cada tema empieza en página nueva**: automático; toda sección abre
  página, como los capítulos de un libro.
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

Todos los entornos (salvo la excepción de `definicion` más abajo)
admiten la nota opcional `\begin{teorema}[Nombre]`, se numeran por
sección y se referencian con `\cref`:

`teorema`, `lema`, `corolario`, `propiedad`, `axioma`,
`criterio` (comparten el contador del teorema), `definicion`, `ejemplo`,
`observacion`, `nota`, `conjetura`, `problema`, `notacion` (cada uno con
su contador), `demostracion` (sin numerar, con `\qed` automático) y
`resolucion` (sin numerar, **sin** QED).

Los **encabezados van abreviados como en mis apuntes a mano**: «Def.: 1.1»,
«Ej.: 1.2», «Obs.: 1.3», «Prop.: 1.4» y «Dem.:» para las demostraciones;
los nombres cortos o principales van completos: «Teorema 1.1», «Lema 1.2»,
«Nota», «Notación», «Criterio», «Problema». `cleveref` usa el mismo
sistema: «def. 1.1» y, en plural, «def.s 1.1 y 1.2».

En `definicion`, el argumento opcional **no** es una nota, sino el
término que se está definiendo, y va como nota al **margen izquierdo**
(no entre paréntesis tras el número):
`\begin{definicion}[Hausdorff] … \end{definicion}` escribe «Hausdorff»
en el margen izquierdo, a la altura de la cabecera, con el mismo estilo
que `\notamargen`. Un entorno vacío `\begin{definicion}` funciona igual,
sin nota. Además, la primera mención del concepto DENTRO del cuerpo se
escribe en cursiva con `\emph{…}` (como el cuerpo de las definiciones va
en cursiva, `\emph` invierte y resalta el término en redonda, que es el
contraste buscado).

El entorno **`anidado`** sirve para meter un entorno dentro de otro
(p. ej. un ejemplo que pertenece a una definición): añade una sangría
extra a TODO el bloque anidado, incluida la cabecera del entorno
interior, como a mano:

```latex
\begin{definicion}[Término]
    … texto de la definición …
    \begin{anidado}
        \begin{ejemplo}
            … ejemplo que va dentro de la definición …
        \end{ejemplo}
    \end{anidado}
\end{definicion}
```

Las **demostraciones** se escriben con `\begin{demostracion} …
\end{demostracion}` (o `\begin{demostracion}[Nombre]`) y quedan siempre
pegadas a su resultado: la plantilla evita que salte una página entre un
enunciado y su demostración, y aplica también la sangría francesa. El
encabezado sale exactamente «Dem.: » (los dos puntos ya cierran la
palabra). Al final de las demostraciones va el **cuadrado hueco (QED)
alineado a la derecha**, automático; las resoluciones de problemas **no**
llevan ese cuadrado (se redactan como texto normal o con otros entornos,
sin `\qed`).

Las **resoluciones de problemas** se escriben con
`\begin{resolucion} … \end{resolucion}` (o `\begin{resolucion}[Cabecera]`,
que por defecto es «Resolución»): mismo estilo que las demostraciones,
pero **sin el cuadrado QED**, conforme a mi estilo. Quedan pegadas a su
problema, como las demostraciones a su resultado. (No vale escribir una
resolución como `demostracion`: heredaría el cuadrado.)

Sobre **`\qedhere`** (el comando de amsthm para alinear el cuadrado con
la última fórmula): solo al final de una demostración, uno como máximo,
y colócalo dentro de una `equation`/`align` o al final de la última
línea de texto; nunca como fórmula suelta `$\qedhere$` (dispara un
aviso de amsthm y puede descentrar el cuadrado).

## Cómo redactar los apuntes (mi estilo a mano)

Los apuntes se redactan **en mi estilo manuscrito**: telegráfico y compacto,
con mis abreviaturas literales dentro del cuerpo (no expandidas). Resumen del
sistema (la versión completa y actualizada vive en mi base de conocimiento):

**Abreviaturas y su plural.** La abreviatura lleva punto y el plural
se forma añadiendo `s` tras el punto: `aplic.` → `aplic.s`,
`var. dif.` → `var.s dif.s`. Además, **las palabras derivadas de una
abreviada usan la misma abreviatura** (el contexto desambigua):
«restricciones» → `restric.s`, «definición, definir, definimos» → `def.`,
«binaria» → `bin.`.

| Abreviatura | Palabra | Abreviatura | Palabra |
|---|---|---|---|
| `aplic.` | aplicación | `conj.` / `subconj.` | conjunto / subconjunto |
| `var.` | variable / variedad | `top.` | topología; `top. induc.` = inducida |
| `elem.` | elemento | `dim.` | dimensión |
| `prob.` | problema | `func.` / `obj.` | función / objetivo (`func. obj.`) |
| `prog.` | programación | `resp.` | respectivamente |
| `def.` | definición, definir, definimos | `t.q.` | tal que |
| `esp.` / `e.t.` | espacio / espacio topológico | `i.e.` | es decir |
| `v.d.` | variedad diferenciable | `e.g.` | por ejemplo |
| `s.a.` | sujeto a (programación) | `c.c.` | caso contrario |
| `sup.` | supongamos | `rel.` | relación (de equivalencia) |
| `restric.` | restricción | `bin.` | binario |
| `coef.` | coeficiente | `vect.` | vector, vectorial |
| `nec.` / `innec.` | necesario / innecesario | `fact.` | factible |
| `suf.` / `insuf.` | suficiente / insuficiente | `opt.` | óptimo, óptima |
| `reg.` | regular | `máx.` / `mín.` | máximo / mínimo |
| `cont.` | continua, continuo | `dif.` | diferenciable |

Los adverbios acabados en «-mente» se abrevian con el **adjetivo + `x`**:
«claramente» → `clarax`. El símbolo `#` significa «número de»: «# de
pasos», «# finito de elementos»; «para todo» y «existe» van con sus
símbolos, `\forall` y `\exists`. Las siglas se definen entre paréntesis
en su primer uso (`OC`, `e.t.`, …) y el término inglés se anota también
entre paréntesis: «(TSP) Travelling Salesman Problem».

**Redacción.** Siempre que se pueda, en **impersonal**
(«considérese», «se tiene que»); si no, con **gerundio**
(«considerando»); y solo en último caso en **primera persona del
plural** («consideramos»), aunque el material original venga escrito
de otra forma. Nunca «siguiente»: **«que sigue»**. Nunca «distinto»:
**«diferente»**.

**Notación matemática.** Comparaciones con `\leqslant` y `\geqslant`
(nunca `\leq` ni `\geq`); conjunto vacío con `\varnothing` (nunca
`\emptyset`); conectivas lógicas con las palabras **«o» e «y»**
(nunca `\vee` ni `\wedge`); productos de «letras» con `\cdot` entre
ellas (`$x\cdot y\cdot z$`) para no confundirlos con variables de
varias letras; vectores **subrayados** (la plantilla redefine `\vec`
para subrayar, así que `$\vec{x}$` sale con la letra subrayada, nunca
con flecha); y definiciones por trozos con **coma entre cada valor
y su condición**: `$x_j = \begin{cases} 1, & \text{si …} \\ 0, & c.c.\end{cases}$`.

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
(cada binaria por casos, con la coma entre valor y condición:
`x_j = {1, si …; 0, c.c.}`) → **Func. obj.** (`min`/`max`) →
**Restricciones** (`s.a.`), y **cada restricción con su comentario
explicativo entre paréntesis** a la derecha: `Σ a_ij x_j ⩾ 1, ∀i
(Todos los clientes cubiertos)`. Los algoritmos se iteran a mano en los
apuntes (`Iter 1. Restric. 1: …`) con la decisión al margen y el criterio
de parada escrito en palabras.

**Márgenes.** Con `\notamargen{}`: aclaraciones de figuras («proy.
estereográfica desde el polo norte»), avisos («No confundir con…»),
vértices «Sí/No actualizamos», y las preguntas pendientes («Esto no está
bien del todo, ¿por qué? Preguntar al prof.»).

## Detalles técnicos (para escribir sin sobresaltos)

- **TikZ con flechas**: escribe `->`, `<->`, `>=` etc. con total
  normalidad. La plantilla carga `tikzlibrary babel`, que neutraliza los
  caracteres abreviados que babel `spanish` activa (`<`, `>`, `"`, `.`)
  dentro de TikZ; sin ella, cualquier `\draw[->]` revienta con un error
  que no apunta en absoluto al preámbulo (habla de `\pgfkeys@splitter`,
  «nullfont», etc.). Van también cargadas `arrows.meta` (flechas
  modernas), `calc` (coordenadas por interpolación
  `($(a)!0.5!(b)$`), `decorations.markings` (marcas sobre curvas) y
  `patterns` (rellenos de gris), que cubren prácticamente cualquier
  figura de apuntes.
- **Matrices anchas**: se permiten hasta **20 columnas**; el preámbulo
  fija `\setcounter{MaxMatrixCols}{20}` (amsmath limita a 10 por
  defecto, y las matrices de incidencia en optimización combinatoria lo
  superan). El nombre del contador va CON MAYÚSCULAS: en minúsculas es
  un error duro de LaTeX. No cambies el valor a mano en el contenido:
  pide más columnas ampliándolo en `main.tex`.
- **Símbolos que faltan en Fira Math**: `⋂ ⋃ ∖ △ ▷ ◁ ⋆` (y también
  los puntos en diagonal de matrices, `\vdots` y `\ddots`) los aporta
  automáticamente Latin Modern Math, fijado en el preámbulo con un
  `range=` de `unicode-math` (Fira Math no los trae, y un glifo ausente
  sale EN BLANCO en el PDF, no sustituido). Si el log avisara «Missing
  character» de otro símbolo, añádelo a ese `range`, con su nombre
  primario de unicode-math (`\triangle` es alias; el primario es
  `\bigtriangleup`). Evita `\vartriangle`, `\subseteqq`, `\supseteqq`,
  `\subsetneqq` y `\supsetneqq`: no están ni en Fira Math ni en Latin
  Modern Math (usa `\triangle`, `\subseteq`, `\subsetneq`, que sí
  están). Regla general: los símbolos matemáticos, como comandos
  (`\bigcup`, `\setminus`), nunca como caracteres Unicode literales
  (⋃, △): con `unicode-math` acaban en el mismo hueco de fuente y
  fallan igual, pero los comandos son localizables con `grep` y quedan
  cubiertos por el respaldo si este se amplía.
- **Divisas y marcas**: `\euro{}` (eurosym) para euros, p. ej.
  `27\,\euro{}` por tonelada; `\ding{51}` (sí) y `\ding{55}` (no)
  (pifont), en blanco y negro, para comprobaciones de factibilidad,
  iteraciones de algoritmos y tablas.
- **Líneas que desbordan**: el preámbulo fija
  `\emergencystretch` a `1em`, que solo entra en juego cuando una línea
  no encuentra punto de corte y de otro modo desbordaría el margen
  (Fira Sans es ancha). Aun así, evita los tres patrones que más overfull
  provocan: listas de tuplas largas dentro de un único inline math
  (mételas en display o como texto, que se parte solo), comentarios entre
  paréntesis kilométricos en filas de `align` (comentario corto; la
  explicación, en prosa) y funciones objetivo sin partir en trozos con
  `\\`. Un overfull de más de 100 pt es un error que hay que arreglar;
  de menos de 10 pt es cosmético.

## Cómo leer el log (avisos benignos)

Al compilar aparecen avisos que NO son errores y no hay que perseguir:

- `Invalid UTF-8 byte or sequence … replaced by U+FFFD` en
  `algorithm.sty`: un comentario en Latin-1 dentro de ese paquete;
  benigno y no arreglable desde el proyecto. (El mismo aviso de
  `anyfontsize.sty` desapareció al eliminar el paquete, que no hacía
  nada útil bajo fontspec.)
- `First Aid for cleveref.sty applied!`: rutina de auto-reparación de
  hyperref/cleveref; funciona como debe.
- `Package hyperref Info: bookmark level for unknown algorithm
  defaults to 0`: cosmético; hyperref no conoce el nivel de marcador
  del flotante `algorithm`.
- Los `marginnote Info: xpos seems to be …`: trazas internas de
  marginnote.
- `Package fontspec Info: Could not resolve font "Fira Math/B"`:
  Fira Math no tiene negrita y unicode-math busca una por defecto;
  recurre a la normal. Sin impacto.
- `Font shape 'TU/FiraMath' will be scaled to size …`: escalado
  normal de las fuentes matemáticas OpenType con rangos ópticos.
- `Package hyperref Warning: Token not allowed in a PDF string
  (removing math shift / superscript)`: los `$` y `^` de un título
  con mates sin `\texorpdfstring`; hyperref los quita y el marcador
  sale igual, pero la regla del `texorpdfstring` los evita del todo.
- `LaTeX Encoding Info: Redeclaring text command \ij …` de babel:
  rutina normal al cargar babel.
- `babel … Making " an active character / Making . an active character`:
  comportamiento normal de babel spanish (y la razón por la que la
  plantilla carga la librería `babel` de TikZ).

En cambio, **«Missing character»** no es benigno: ese glifo está saliendo
en blanco; véanse los símbolos con respaldo más arriba.

## Reglas para generar contenido con un LLM

Bloque para pegar en el prompt junto al material de la asignatura:

1. Matemáticas siempre con comandos (`\bigcup`, `\setminus`,
   `\triangle`), nunca con caracteres Unicode matemáticos literales
   (⋃, △, →), ni siquiera en notas al margen o `caption`: la fuente de
   texto no los tiene y salen en blanco. Nada de `$$`: usa `\[ \]`,
   `equation*` o `align*`.
2. TikZ: la plantilla ya carga `\usetikzlibrary{babel}` (más
   `arrows.meta`, `calc`, `decorations.markings` y `patterns`);
   escribe `->` con normalidad. Nada de `\shorthandoff` manual.
3. **Títulos con mates**: `\texorpdfstring{$\mathbb{R}P^2$}{RP2}`.
   El preámbulo lleva una red de seguridad para los marcadores, pero
   los `$` y `^` de un título sin `texorpdfstring` dejan avisos
   («Token not allowed in a PDF string»).
4. **Títulos que caben en una línea**: sin fórmulas largas ni más de
   ~50 caracteres; el prefijo automático «Tema N.» ya resta espacio y
   los saltos de línea en títulos quedan fuera de estilo.
5. Matrices de más de 10 columnas: permitidas (el preámbulo fija
   `MaxMatrixCols` a 20). No toques el contador a mano.
6. Comentarios en filas de `align`: cortos, dentro de `(\text{...})`;
   la explicación larga, en prosa después. Parte las funciones
   objetivo largas con `\\`.
7. Enumeraciones y tuplas largas: como texto o en display, jamás dentro
   de un único inline math. Una fórmula inline de más de ~15 caracteres
   no tiene puntos de ruptura: si no cabe, vete al display; y deja
   texto suficiente alrededor de cada fórmula para que la línea tenga
   dónde romper.
8. **Figuras TikZ**: dibuja la geometría completa (una recta que debe
   cortar un eje, se dibuja hasta el eje; las intersecciones se
   calculan, que es geometría y no decoración); etiquetas con anclaje
   explícito (`node[above left]`, `node[right]`,…) y separadas entre
   sí: Fira Sans es más ancha que Computer Modern y lo que «parece
   que cabe» se solapa en el papel; si una etiqueta conceptual queda
   atravesada por un eje, muévela a zona despoblada y señala el punto
   con una flecha fina gris. Tras compilar, MIRA el render de cada
   figura: los solapes de etiquetas NO aparecen en el log.
9. `\qedhere`: a lo sumo uno por demostración, al final de una display o
   de la última línea de texto; nunca `$\qedhere$`. Las resoluciones van
   en `resolucion` (sin QED), no en `demostracion`.
10. Divisas con `\euro{}` (eurosym); marcas sí/no con `\ding{51}` y
   `\ding{55}` (pifont).
11. Referencias cruzadas: solo `\cref`/`\Cref`; etiquetas sin tildes ni
   espacios (`prob:t4-01`, `fig:grafo-match`).
12. Paquetes ya disponibles (no cargues otros): tikz (+librerías babel,
   arrows.meta, calc, decorations.markings, patterns), amsmath,
   amsthm, unicode-math, geometry, csquotes, tocloft, marginnote,
   needspace, etoolbox, algorithm/algpseudocode, listings, xcolor,
   eurosym, pifont, hyperref, bookmark, cleveref.
13. Un overfull que sobreviva a `\emergencystretch` se arregla
   reescribiendo la frase (más corta, con palabras de separación), no
   tocando la plantilla. Como umbral: más de 100 pt es un error que
   debes arreglar; menos de 10 pt es tolerable.
14. Definiciones: `\begin{definicion}[Término]` (término al margen
   izquierdo) y la primera mención del concepto en el cuerpo con
   `\emph{Término}`.
15. Vectores: `\vec{x}`, `\vec{u}\cdot\vec{v}`… (la plantilla
   redefine `\vec` a subrayado); nunca `\overrightarrow` ni negrita.
16. Un tema = una `\section` (que abre página nueva automáticamente);
   no metas `\clearpage` manuales entre temas.

## Recomendaciones

- Usa `\cref` / `\Cref` (cleveref) para todas las referencias cruzadas:
  los nombres ya siguen el sistema de abreviaturas (teorema, def., ej.).
- Las notas al margen (`\marginpar` o `marginnote`) sirven para
  mini-índices de términos y referencias cruzadas, como en el Diestel.
- Los símbolos matemáticos los aporta *Fira Math* a través de
  `unicode-math` (por eso la plantilla no carga `amssymb`); `\mathbb`,
  `\mathcal`, etc. funcionan igual. Los pocos que faltan en Fira Math
  (`\bigcup`, `\triangle`, `\setminus`,…) vienen de Latin Modern Math
  (véanse los «Detalles técnicos»).
- Pensada para imprimirse en A4 y en blanco y negro: evita colores salvo
  que aporten algo pedagógico.
