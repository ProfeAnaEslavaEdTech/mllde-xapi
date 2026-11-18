# Revisión a mano del inventario de descriptores · 18 nov 2026

**Qué se revisó:** los 382 descriptores del inventario publicado (`index.html` de `main`, idéntico al zip del 18 nov), uno por uno, a mano:
- 115 de gramática;
- 96 de vocabulario;
- 100 de habla;
- 71 de mediación.

**Qué no se hizo:** cotejar cada descriptor con la hoja oficial *CEFR Descriptors (2020)* (H9). Sigue pendiente.

## 1. Can-do mal formados: 66, todos de gramática

**El fallo:** el *can-do* empieza por «Can» seguido de un sustantivo, no de un verbo. Por ejemplo, «Can unfinished/relevant-now vs finished time using…» o «Can location using…».

**El origen:** el texto se generó con la plantilla «Can {función} using: {forma}» y metió el nombre de la función donde iba un verbo. Es el hallazgo H10.

| Nivel | Mal formados | De |
|---|---|---|
| A1 | 6 | 21 |
| A2 | 20 | 25 |
| B1 | 14 | 23 |
| B2 | 10 | 20 |
| C1 | 10 | 16 |
| C2 | 6 | 10 |
| **Total** | **66** | **115** |

- **B1–C1:** 34 de 59.
- **Vocabulario, habla y mediación:** todos empiezan bien, por un verbo.

**Corrección de mi recuento automático:** el total coincidía, 66, pero por dos errores que se compensaban:
- `en.gram.c1.passive-reporting` («Can distance/attribute a claim…») **está bien**: *distance* y *attribute* son verbos;
- `en.gram.b2.result-so-such` («Can cause and consequence…») **está mal** y se me había escapado.

**La propuesta de corrección** está en `can-do_mal_formados_y_propuesta.csv` (en esta carpeta):
- solo cambia la función, lo que va antes de «using:»;
- la forma no se toca;
- ejemplo: «Can distinguish unfinished or relevant-now time from finished time using: present perfect vs past simple».

## 2. Otros hallazgos

| # | Descriptor | Hallazgo | Por qué importa |
|---|---|---|---|
| 1 | `en.gram.b2.future-perfect-cont` | El id dice «continuo», la forma mezcla los dos («will have (been) + pp/-ing») y el ejemplo usa el simple («we'll have shipped») | La IA no sabe si cuenta el simple. Hay que separarlos o renombrar la descripción (el id no se renombra) |
| 2 | `en.gram.c2.idiomatic-collocation` | Su ejemplo, «dead in the water», es el descriptor de vocabulario `en.voc.c2.dead-in-the-water` | Una misma frase puede contar dos veces |
| 3 | `en.gram.c2.connotative-precision` | Su ejemplo, «streamlined», es `en.voc.c2.streamline` | Lo mismo |
| 4 | `en.voc.c1.economies-of-scale` | El ejemplo no contiene el término: «Scale gave them economies we can't match» | No sirve de ejemplo de evidencia |
| 5 | `en.voc.b2.benchmark` | Se define como sustantivo («a standard used for comparison») y el ejemplo lo usa como verbo («We benchmark against…») | No se sabe qué uso cuenta |
| 6 | `en.voc.c1.penetration` | El término es «market penetration» y el ejemplo dice solo «Penetration» | Lo mismo |
| 7 | `en.gram.a2.prep-movement` | El ejemplo es figurado («moved into the red»), no de movimiento físico | Es un mal modelo para A2 |
| 8 | `en.gram.b1.relative-whose` y `en.gram.c1.complex-np` | El ejemplo es un fragmento, no una frase | Menor |
| 9 | `en.gram.b2.hedging-disagreement` | Está en gramática, pero es pragmática (discurso) y roza el habla | Necesita una frontera clara con el habla |
| 10 | Vocabulario A1 | Dice «work context»; los demás niveles, «business context» | Menor; conviene unificar |
| 11 | Ids con «-ize» y con «-ise» | `summarize-discussion`, `summarize-simple`, `summarize-report`, `synthesize-sources`, `synthesize-multivoice` frente a `synthesise-sources` (C2) | Los ids no se renombran (son estables). Solo se anota |

## 3. Un error mío, ya corregido

En la lista de trabajo de B1–C1, la etiqueta «nuevo v0.7.2» de la página se había pegado al id de 40 descriptores. Los ids publicados están bien.

La lista ya está corregida y tiene una columna nueva, `nuevo_en_v0.7.2`. La columna «can-do mal formado» se ha rehecho con esta revisión a mano.

## 4. Qué se hace con esto

- **`main` no se toca:** es el anexo publicado.
- **Las correcciones van a la propuesta de la v0.8.4**, en la rama, para que la autora las apruebe (Q24).
- **Se corrigen antes de medir con estos descriptores.** Un *can-do* sin verbo no dice qué tiene que hacer el alumno, y la IA no tiene contra qué comparar.
