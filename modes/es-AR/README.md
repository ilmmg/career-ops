# career-ops -- Modo de mercado Argentina (`modes/es-AR/`)

Capa de mercado para candidatos que viven en **Argentina**: empleo local (relación de dependencia, monotributo) y trabajo remoto para empresas del exterior (contractor, cobro en dólares).

Como `modes/sg/`, no es una traducción: son los modos canónicos más una capa con las reglas del mercado argentino. La traducción al español ya está en `modes/es/`, pero sus reglas de mercado son las de España (14 pagas, IRPF, Seguridad Social, contrato indefinido), que no aplican en Argentina.

## ¿Cuándo usar estos modos?

Usá `modes/es-AR/` si se cumple al menos una de estas condiciones:

- Vivís en Argentina y buscás trabajo en el país o remoto desde acá.
- Necesitás comparar ofertas en **pesos y en dólares**, en **bruto mensual con aguinaldo** o como **contractor** que factura con monotributo.
- Querés saber, antes de puntuar, si un aviso remoto **contrata desde Argentina** y si **te alcanza el nivel de inglés** que pide.

Si vivís en otro país de habla hispana, quedate con `modes/es/` o con los modos estándar de `modes/`.

## ¿Cómo activarlos?

### Opción 1 -- Por sesión

Decile al agente al inicio de la sesión:

> "Usá los modos del mercado argentino de `modes/es-AR/`."

### Opción 2 -- De forma permanente

Agregá en `config/profile.yml`:

```yaml
language:
  output: es
  modes_dir: modes/es-AR
```

`language.output` decide el idioma de lo que se escribe (informes, CV, cartas); `modes_dir` aporta las reglas del mercado. Si buscás en paralelo en otro mercado, declaralos los dos (`modes_dir: [modes/es-AR, modes]`): el primero aporta el modo de evaluación, y el mercado de cada aviso se decide por sus propias señales (ver AGENTS.md → "Output Language vs Market Modes").

Para que el chequeo de autorización de trabajo funcione, completá también en `config/profile.yml` `location.authorized_in: ["Argentina"]` (más cualquier país donde ya tengas permiso de trabajo) y `location.needs_sponsorship: true` si para trabajar en relación de dependencia en otro país necesitarías una visa. Poné tu nivel de idiomas en `cv.md`: el Language Gate lo lee de ahí.

## ¿Qué modos cubre?

| Archivo | Basado en | Rol |
|---------|-----------|-----|
| `_shared.md` | `modes/_shared.md` | Vocabulario del mercado, elegibilidad remota desde Argentina, Language Gate, normalización de sueldos, estafas frecuentes |
| `oferta.md` | `modes/oferta.md` | Evaluación A-H con los agregados argentinos (Bloques A, B, D, F y G, y encabezado del informe) |
| `aplicar.md` | `modes/apply.md` | Formularios de postulación con las preguntas típicas del mercado local |
| `pipeline.md` | `modes/pipeline.md` | Bandeja de avisos con los chequeos argentinos antes de cada evaluación |

Los demás modos (`scan`, `batch`, `pdf`, `cover`, `tracker`, `interview-prep`, etc.) se usan desde `modes/`: su contenido es de herramientas y de flujo, no de mercado.

## Dónde buscar

- **HiringRoom:** muchas empresas argentinas publican en `<empresa>.hiringroom.com`; se agregan como `tracked_companies` (el proveedor las detecta solo). Para pasar de nombres de empresas a portales, usá el modo `discover`.
- **Get on Board** (`provider: getonbrd`): avisos de tecnología, con mucho remoto para LATAM.
- **Computrabajo:** el proveedor acepta cualquier `<país>.computrabajo.com`; el host argentino (`ar.computrabajo.com`) todavía no se midió.
- **Portales remotos** (Remotive, Himalayas, Working Nomads, We Work Remotely, Jobicy): filtrá por ubicación con `location_filter`, porque muchos avisos son "US only".
- **LinkedIn:** las alertas de empleo por mail se importan con `node linkedin-import.mjs --file alerta.eml` (sin scraping; ver la guarda de LinkedIn en AGENTS.md).

## Créditos

La idea del Language Gate (comparar el idioma que exige el rol con el nivel declarado, antes de puntuar) está adaptada de [ai-job-search](https://github.com/ai-job-search-dev/ai-job-search) (MIT).

## Contribuir

Para mejorar estos modos, seguí `CONTRIBUTING.md`. Cualquier dato normativo nuevo (porcentajes, plazos, regímenes) tiene que venir con una fuente oficial y la fecha en que se verificó.
