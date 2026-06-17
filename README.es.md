[English](README.md) | [한국어](README.ko.md) | **Español** | [Français](README.fr.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [Tiếng Việt](README.vi.md)

# teach-me-a-lesson — una skill de profesor paciente y cercano para principiantes en IA y programación

Una [skill de Claude](https://docs.claude.com/en/docs/claude-code/skills) que explica Claude, las herramientas de IA y los conceptos de programación/informática **como lo haría un buen profesor para principiantes totales y personas sin experiencia técnica**, y que te sigue ayudando mientras trabajas.

En lugar de soltar la respuesta sin más, se centra en crear ese momento de **«¡ah, *así que era eso*!»** con una sola buena analogía.

## Qué hace

Funciona en seis modos (los activas con solo pedirlo, o con un comando de barra).

| Modo | Comando | Qué hace |
|------|---------|----------|
| **explain** | `/tl-explain <tema>` | Explica un concepto con analogías, tablas y conclusiones clave (por defecto) |
| **mistake** | `/tl-mistake` | Diagnostica qué salió mal y por qué —sin culpar— y cómo arreglarlo |
| **bad-habit** | `/tl-bad-habit` | Detecta malos hábitos recurrentes y sugiere mejores formas de hacerlo |
| **knowledge** | `/tl-knowledge <tema>` | Guarda lo que acabas de aprender como archivo de conocimiento (nota markdown) |
| **token** | `/tl-token` | Observa cómo trabajas y señala el desperdicio de tokens/contexto, con soluciones concretas |
| **config** | `/tl-config` | Configura el idioma, el registro, el tono/persona, el nivel de emojis y cómo se dirige a ti |

Mientras la skill está cargada, también actúa como **ayudante siempre presente**: cuando ve acciones arriesgadas (pegar comandos desconocidos, exponer claves de API, operaciones irreversibles), peticiones basadas en un malentendido o un camino ineficiente, lo **señala con suavidad** —sin dar la lata— y te deja a ti la decisión.

> Nota: la ayuda continua funciona mientras la skill está cargada (dentro del contexto de la conversación). No es un hook que revise automáticamente cada entrada.

### Ejemplos que la activan

- «Explícame qué es MCP, muy sencillo: soy principiante total»
- «Siempre confundo API y SDK. Explícame la diferencia con una analogía»
- «Las terminales me dan miedo, ¿de verdad tengo que usar una?»
- «Creo que acabo de subir mi .env a GitHub, ¿cuál es el problema?» → mistake
- «Señala mis malos hábitos» → bad-habit
- «Siento que estoy quemando tokens, ¿le echas un vistazo?» → token

## Instalación

### 1) Copia la carpeta de la skill

```bash
# macOS / Linux
cp -r teach-me-a-lesson ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse teach-me-a-lesson $env:USERPROFILE\.claude\skills\
```

### 2) Instala los comandos de barra (opcional, para usar /tl-*)

Copia los archivos de la carpeta `commands/` de la skill en tu carpeta de comandos.

```bash
# macOS / Linux
cp teach-me-a-lesson/commands/tl-*.md ~/.claude/commands/

# Windows (PowerShell)
Copy-Item teach-me-a-lesson\commands\tl-*.md $env:USERPROFILE\.claude\commands\
```

La skill también se activa automáticamente con frases sencillas como «explícame esto de forma simple». Los comandos son solo una forma cómoda de llamar a un modo concreto de manera explícita.

## (Opcional) Conecta tus propios archivos de conocimiento

Si tienes **archivos de conocimiento** (una carpeta de notas markdown), la skill los usa como fuente principal. Si no los tienes, recurre al conocimiento propio de Claude, así que **funciona perfectamente sin ningún archivo de conocimiento**.

- Carpeta predeterminada de búsqueda/guardado: `./knowledge/` en tu directorio de trabajo, o `~/.claude/teach-me-a-lesson/knowledge/`
- Si ya tienes una carpeta de notas, solo apunta ahí.
- Para las reglas detalladas y el formato de índice opcional, consulta `references/knowledge-files.md`.

> Este repositorio **no** incluye ningún documento de conocimiento personal. Solo se publica la metodología de enseñanza (la skill en sí).

## Ajustar el tono y el idioma

Puedes ajustar el **idioma, el registro y el estilo** del profesor a tu gusto. Por ejemplo, en coreano ajusta no solo la formalidad (존댓말/반말), sino también el **ambiente** (cálido, sobrio, animado, formal).

- `/tl-config` — pregunta por turnos: idioma → registro → tono/persona → nivel de emojis → cómo dirigirse a ti, y lo guarda
- También funciona en lenguaje natural: «háblame de tú y con energía», «explícame en inglés», «menos emojis»
- Los ajustes se guardan en `~/.claude/teach-me-a-lesson/config.json` (un archivo de tono personal, por eso **no** se incluye en la distribución). Sin ajustes, funciona con los **valores por defecto (profesor cálido, coreano cortés 해요체)**.
- Sea cual sea el tono, la calidad de la enseñanza (analogías, sin culpar, sin saturar, citando fuentes) se mantiene. Consulta `references/tone-config.md`.

## Estructura

```
teach-me-a-lesson/
├── SKILL.md                      # Activadores + 6 modos + ayuda continua + config de tono + flujo
├── references/
│   ├── teaching-style.md         # Cómo crear analogías, buenos/malos ejemplos, correcciones suaves
│   ├── knowledge-files.md        # Reglas de búsqueda/guardado de archivos de conocimiento (genérico)
│   ├── modes.md                  # Los 6 modos en detalle + ejemplos de ayuda continua
│   └── tone-config.md            # Esquema y personas de idioma/registro/tono/emojis/trato
├── commands/                     # Comandos de barra /tl-* (cópialos en tu carpeta de comandos)
├── evals/
│   └── evals.json
├── README.md                     # Inglés (por defecto)
├── README.{ko,es,fr,zh,ja,vi}.md # Traducciones (KO/ES/FR/ZH/JA/VI)
└── LICENSE
```

## Licencia

Licencia MIT. Úsala, modifícala y redistribúyela libremente.
