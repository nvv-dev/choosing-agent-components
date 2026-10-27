# choosing-agent-components

> ¿Skill, subagente, hook, MCP o una línea en CLAUDE.md?

**Elegir la pieza más liviana** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Árbol de decisión para agregar una capacidad o una regla a un setup de agentes eligiendo la pieza más barata que funcione: nada, una herramienta determinista (linter, prueba), un hook, una línea de CLAUDE.md, una skill, un comando, un subagente, un servidor MCP o un plugin.

## Objetivo

Ahorrar tokens y mantenimiento desde el diseño.

## Cuándo usarla

- Vas a crear una skill, agente, hook o integración nueva

## Cuándo no

- Cuando ya sabes exactamente qué pieza necesitas

## Ejemplo

```text
/choosing-agent-components Quiero que el agente nunca haga push a main.
```

## Cómo se activa

Esta skill **solo se activa a mano** (`disable-model-invocation: true`): no ocupa contexto en cada sesión y la invocas cuando la necesitas:

- Instalada como plugin: `/choosing-agent-components:choosing-agent-components`
- Copiada a `.claude/skills/`: `/choosing-agent-components`

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install choosing-agent-components@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `agent-guardrails@nvvdev` en su lugar (incluye esta skill y las demás de [agent-guardrails](https://github.com/nvv-dev/agent-guardrails)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/choosing-agent-components.git /tmp/choosing-agent-components
mkdir -p .claude/skills
cp -R /tmp/choosing-agent-components/skills/choosing-agent-components .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/choosing-agent-components/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/choosing-agent-components
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `choosing-agent-components` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall choosing-agent-components@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/choosing-agent-components`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/choosing-agent-components/SKILL.md`](skills/choosing-agent-components/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/choosing-agent-components/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/agent-guardrails](https://github.com/nvv-dev/agent-guardrails), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [Hainrixz/claude-anatomy](https://github.com/Hainrixz/claude-anatomy).

## Licencia

MIT.

---

## English

**choosing-agent-components** — A decision order from 'nothing' to 'plugin' that picks the cheapest component that reliably does the job.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install choosing-agent-components@nvvdev`, or copy `skills/choosing-agent-components/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/choosing-agent-components`. Manual-only skill: invoke it with `/choosing-agent-components:choosing-agent-components` (plugin) or `/choosing-agent-components` (copied). Canonical source: [nvv-dev/agent-guardrails](https://github.com/nvv-dev/agent-guardrails). License: MIT.
