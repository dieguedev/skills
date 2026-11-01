Conjunto de skills que utilizo en mi día a día desarrollando.

## Instalación

Elige **un solo método** por agente: instalar ambos duplica cada skill.

### Claude Code plugin

El plugin se actualiza automáticamente con cada actualización.

```
/plugin marketplace add dieguedev/skills
/plugin install skills@dieguedev
```

### Otros agentes

Requiere Node.js 22.20 o superior. Hay que actualizar las skills de forma manual con `npx skills@latest update`

Para instalar las skills:

```
npx skills@latest add dieguedev/skills -a codex
```

Si omites `-a`, el instalador te pregunta el agente de forma interactiva.

#### Opciones útiles

| Opción                  | Qué hace                                                      |
| ----------------------- | ------------------------------------------------------------- |
| `-a, --agent <agentes>` | Agente(s) donde instalar. `'*'` los incluye todos.            |
| `-s, --skill <skills>`  | Instala solo las skills indicadas, por ejemplo `-s grill-me`. |
| `-l, --list`            | Lista las skills del repo sin instalar nada.                  |
| `-g, --global`          | Instala a nivel de usuario en lugar de en el proyecto actual. |
| `--copy`                | Copia los archivos en lugar de crear enlaces simbólicos.      |
| `-y, --yes`             | Salta las confirmaciones.                                     |

Ejemplos:

```
# Ver qué skills hay sin instalar
npx skills@latest add dieguedev/skills --list

# Instalar solo grill-me en Claude Code y Cursor
npx skills@latest add dieguedev/skills -s grill-me -a claude-code -a cursor

# Probar una skill sin instalarla (sin --agent, solo imprime el prompt)
npx skills@latest use dieguedev/skills@grill-me --agent claude-code
```

#### Identificadores de agente más comunes

| Agente         | Identificador    |
| -------------- | ---------------- |
| Claude Code    | `claude-code`    |
| Codex          | `codex`          |
| Cursor         | `cursor`         |
| Gemini CLI     | `gemini-cli`     |
| GitHub Copilot | `github-copilot` |
| OpenCode       | `opencode`       |
| Windsurf       | `windsurf`       |
| Amp            | `amp`            |
| Cline          | `cline`          |
| Roo            | `roo`            |
| Goose          | `goose`          |
| Devin          | `devin`          |
| Kiro CLI       | `kiro-cli`       |

La lista completa está en la [documentación de `skills`](https://github.com/vercel-labs/skills/blob/main/docs/agents.md).

#### Dónde se instalan

Por defecto en el proyecto actual. Si utilizas `-g`, en tu carpeta de usuario. La mayoría de agentes leen `.agents/skills/`. Claude Code usa `.claude/skills/`.
