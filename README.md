# test-3239188-simple-stock-flow-doc

> **Reto SDD · Ficha ADSO 3239188**
> Entrega: **hoy 8 de octubre de 2026, a las 10:50 p. m. (hora Colombia)**. Cuenta regresiva: https://claude.ai/artifact/3ja3TMwGnprBV6QCcyAruT

Este reto **no se hace en el repositorio principal de su proyecto**. Se hace en un **fork de este repositorio**.

## Qué hay que hacer

El único insumo es el modelo de datos de *Simple Stock Flow*: [`spec/data-model.md`](spec/data-model.md).
A partir de él se reconstruye la documentación del sistema **hacia atrás**, de la arquitectura al contexto:

| Orden | Carpeta | Qué se produce a partir del modelo de datos |
|---|---|---|
| 1 | `05-architecture/` | Estilo y piezas del sistema que el modelo implica (agregados, puertos, dónde vive cada regla) |
| 2 | `04-requirements/` | Historias de usuario y requisitos no funcionales que el modelo hace necesarios |
| 3 | `03-product/` | Problema que resuelve y visión del producto |
| 4 | `02-domain/` | Entidades, reglas y eventos del dominio, con su glosario |
| 5 | `01-context/` | Descripción general y alcance (qué se construye y qué no) |
| 6 | `05-architecture/` (cierre) | Volver a la arquitectura y comprobar que cuadra con todo lo anterior y con el modelo |

La carpeta `06-data/` **no se escribe**: es el modelo que se les entrega.

## Reglas

1. Hagan **fork** de este repositorio a su cuenta o a la de su equipo.
2. Trabajen en su fork. Una carpeta por documento, con los nombres de la tabla de arriba.
3. Cada afirmación debe poder rastrearse al modelo de datos (cite la sección, por ejemplo «§2.3» o «FK-2»).
   Si algo no sale del modelo, márquenlo como **supuesto**.
4. Lo que cuenta es el **último commit anterior a las 10:50 p. m.** Lo que llegue después no se revisa.
5. Se evalúa el desempeño con SDD: cómo se lee, se interpreta y se aplica la especificación. No el volumen de texto.

## En qué semana va cada equipo

Se calculó comparando cada repositorio `-docs` con la plantilla de gobernanza. Las semanas son las de
`00-sdd-guide.md`: semana 1 contexto y dominio (01-02), semana 2 producto y requisitos (03-04),
semanas 2-3 arquitectura y datos (05-06), semanas 3-4 diseño detallado (07 en adelante).

| Equipo (proyecto) | Semana en la que va | Lo que ya tiene |
|---|---|---|
| lexia | 3-4 | 01 a 06 y 07-api |
| fixgo | 2-3 | 01 a 06 |
| smart-technical-service-to-professional | 2-3 | 01 a 06 |
| belleza-ya | 2-3 | 01 a 06 |
| distrilink | 2 | 01 a 04; falta 05 |
| interemprendedores | 2 | 01 a 04; falta 05 |
| construction-project-management-system | 1 | solo 01-context |
| residential-complex | sin empezar | sin cambios sobre la plantilla |
| huila-travel-expedition | sin empezar | sin cambios sobre la plantilla |
| huila-travel-services | sin empezar | sin cambios sobre la plantilla |
| fastbill-manager | sin empezar | sin cambios sobre la plantilla |

Es una estimación por archivos modificados en `main`. Si su equipo trabajó en otra rama, avísenlo.

## Nota sobre el modelo de datos

`spec/data-model.md` enlaza a otros documentos del spec original (`constitution.md`, `plan.md`, `adr/`, etc.).
**No se entregan**: esos enlaces no abren. Todo lo que necesitan está en el modelo.
