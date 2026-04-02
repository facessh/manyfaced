# manyfaced

> A catalog of agent skills where every step is run by a specialized face.

Manyfaced skills are agent skills (Claude Code, OpenClaw) where the generic AI
voice has been replaced with faces — cognitive primitives that change how an LLM
composes language. Each step that requires judgment is routed to a face or team
of faces. Mechanical steps stay faceless.

Every skill includes a **circuit diagram** showing the routing logic at a glance:
rectangles are faceless plumbing, rounded boxes are solo faces, hexagons are
teams. The diagram is the architecture.

## Browse the catalog

| Skill | What it does | Circuit |
|-------|-------------|---------|
| *your skill here* | — | — |

## Install a manyfaced skill

**Via the faces CLI** (recommended):

```bash
# Browse available skills
faces catalog:manyfaced

# See details for a skill
faces catalog:manyfaced --skill manyfaced-code-review

# Install to Claude Code
faces catalog:manyfaced --install manyfaced-code-review --skills-dir ~/.claude/skills

# Install to OpenClaw
faces catalog:manyfaced --install manyfaced-code-review --skills-dir ~/.openclaw/workspace/skills
```

The install command copies FACE.md files to `~/.faces/catalog/` and prints
which faces need compilation.

**Manual install:**

```bash
git clone --depth 1 https://github.com/facessh/manyfaced.git ~/manyfaced
cp -r ~/manyfaced/<skill-name> ~/.claude/skills/<skill-name>
```

Before using a manyfaced skill, compile its faces. Each skill has a Setup
section listing which faces need compilation and where the FACE.md files are.

## Requirements

- [faces-skill](https://github.com/facessh/faces-skill) — the `/faces`, `/face`,
  `/faceteam`, and `/manyface` slash commands
- [faces CLI](https://www.npmjs.com/package/faces-cli) — `npm install -g faces-cli`
- A [faces.sh](https://faces.sh) account (Free or Connect plan)

## Contributing

Built a manyfaced skill? Submit a PR.

### Skill vs production

A manyfaced skill is a **template** — a reusable workflow with face assignments.
The faces you cast for a specific use case are a **production** — instances of
the template.

When publishing, include only faces that are structural to the skill itself (if
any). Production-specific faces belong to the user, not the catalog. Most skills
will ship with an empty `catalog/` and instructions to run `/face` for each role.

If a skill does ship with structural faces (e.g. a built-in adversarial critic),
include the full FACE.md — frontmatter, Queued sources with real URLs, Sources,
Lessons, Notes. This is the living document that lets someone recreate the face.

### Composite faces

If a skill uses composite faces (Face Math), include:
- FACE.md files for all component faces
- The composite's FACE.md with the `formula` field set (e.g. `"a | b - c"`)
- A note in the composite's Notes section listing which components are required

### Directory structure

```
manyfaced-<skillname>/
  SKILL.md              # the skill — must include a circuit diagram
  catalog/              # FACE.md and TEAM.md files (structural faces only)
    <alias>/FACE.md
    teams/<team-name>/TEAM.md
  README.md             # what the skill does, who it's for, example usage
```

### Requirements for submission

- [ ] Directory named `manyfaced-<skillname>`
- [ ] `SKILL.md` with YAML frontmatter (`name`, `description`)
- [ ] Circuit diagram in mermaid after the Setup section — uses standard
      notation: `[faceless]`, `([solo face])`, `{{team}}`
- [ ] Setup table listing all faces and teams with paths
- [ ] All structural FACE.md files in `catalog/` with queued sources (real URLs)
- [ ] All TEAM.md files in `catalog/teams/` with mermaid protocol diagrams
- [ ] `README.md` explaining the skill, who it's for, and example output
- [ ] No compiled face data — only FACE.md files. Users compile locally.
- [ ] No API keys, tokens, or credentials in any file

### Version tagging

Tag releases with semver git tags (`v1.0.0`, `v1.1.0`). Users can pin to a
version: `git clone --branch v1.0.0 ...`. Breaking changes to the circuit
(adding/removing faces, changing step routing) bump the major version.

### How to create a manyfaced skill

Use the `/manyface` slash command from [faces-skill](https://github.com/facessh/faces-skill).
It walks you through decomposing a skill into roles, casting faces, and
producing the output directory. Choose "publish" at the end to prep for a PR.

---

[faces.sh](https://faces.sh) · [faces-skill](https://github.com/facessh/faces-skill) · [docs](https://docs.faces.sh)
