# schuups/skills

Personal [Claude Code](https://claude.ai/code) skills collection — educational content for family and software development guidelines.

## Plugins

The repo hosts two plugins, installable independently:

| Plugin | Skills | Install when you want |
|--------|--------|-----------------------|
| `family-skills` | `kids-contents`, `kids-school-exercises` | Educational content and exercises for the kids |
| `technology-skills` | `dev-guidelines` | Structured coding discipline for development sessions |

---

## Installation

### Step 1 — Add the marketplace

```bash
claude plugin marketplace add https://github.com/schuups/skills
```

### Step 2 — Install a plugin

```bash
# Family-oriented skills
claude plugin install family-skills@schups-skills

# Technology-oriented skills
claude plugin install technology-skills@schups-skills
```

### Updating

```bash
claude plugin marketplace update schups-skills
claude plugin update family-skills@schups-skills
# or
claude plugin update technology-skills@schups-skills
```

### Uninstalling

```bash
claude plugin uninstall family-skills@schups-skills
# and/or
claude plugin uninstall technology-skills@schups-skills
```

---

## Skills

### `kids-contents`

Generates multi-layered audio stories, discussion guides, and reading lists for a specific child (Quentin, age 9, Zurich). Content is calibrated to his interests in space, physics, and mathematics. The quality target is Feynman-grade engagement: captivating enough to listen to for hours on a roadtrip, interesting for both the child and the parent alongside him.

**When it triggers:**
- A movie, museum visit, or question sparked curiosity
- "Podcast for my son", "story about X for Quentin", "my son asked about..."

**Usage examples:**

```
My son just watched Apollo 13 and he's been asking why they called it a 'successful failure'.
Can you prepare a 20-minute audio story for him? Also a discussion guide and reading list.
```

```
Quentin has been asking 'what is the universe expanding into?' for three days.
Can you make a podcast episode for him? Don't dumb it down — he loves black holes.
```

```
After school Quentin asked what a black hole actually is. Can you create a story and discussion guide?
```

**What you get:**

1. **Pedagogical brief** — the educational strategy and development goals embedded in the content. Review and approve before anything is generated.
2. **Audio story script** — ~20 minutes read aloud, character-driven, Feynman-style. Engaging for both child and parent.
3. **Discussion guide** — 8 question types covering recall, understanding, critical thinking, empathy, counterfactual reasoning, and systems thinking.
4. **Reading / watching list** — curated next steps with difficulty ratings (⭐ to ⭐⭐⭐).

---

### `kids-school-exercises`

Generates printable 30-minute exercise sheets for 4th grade schoolwork (Lehrplan 21, Kanton Zürich). Subjects: Mathematik, Deutsch, Englisch, Natur Mensch Gesellschaft. All content in Hochdeutsch. Sheets are completed on paper; photos of completed sheets are corrected by Claude.

**Three modes:**

**Mode A — Generate from topic:**

```
Quentin hat nächste Woche eine Matheprüfung über schriftliche Multiplikation
(dreistellig × einstellig). Kannst du ein Übungsblatt erstellen?
```

```
Deutsch: Artikel und Pluralformen üben. Er macht da immer noch Fehler.
```

```
Can you create an English exercise sheet on simple present and yes/no questions?
```

**Mode B — Analyse a graded test (attach photo):**

```
[photo of graded test attached]
Quentin hat seinen Deutschtest zurückbekommen. Kannst du die Fehler analysieren
und ein gezieltes Übungsblatt erstellen?
```

**Mode C — Correct a completed sheet (attach photo):**

```
[photo of completed exercise sheet attached]
Kannst du das korrigieren?
```

Each exercise is assessed on three dimensions: correctness, method (intermediate steps shown), and presentation (legibility, alignment). A correct answer without working shown is flagged.

---

### `dev-guidelines`

Enforces deliberate, surgical coding behaviour. Before any code is written, an explicit strategy and verifiable success criterion must be stated. Ambiguous requests are met with a targeted clarifying question, not a default interpretation.

**When it triggers:**
- Any request to write, review, refactor, or fix code

**What changes:**

Without the skill:
> "Clean up the auth module" → Claude starts editing

With the skill:
> "Clean up the auth module" → Claude asks: what specifically should change, what should stay the same, and how do we verify it's done?

**What it enforces:**
- Strategy and goal stated before any code changes
- Minimal, surgical edits — no scope creep, no unsolicited abstractions
- Intermediate steps and roadmap considered before touching anything
- Clarifying questions when the request is ambiguous — no silent interpretation

---

## Repository structure

```
.claude-plugin/
  marketplace.json        # Marketplace manifest (name: schups-skills)
plugins/
  family/
    .claude-plugin/
      plugin.json         # name: family-skills
    skills/
      kids-contents/
      kids-school-exercises/
  technology/
    .claude-plugin/
      plugin.json         # name: technology-skills
    skills/
      dev-guidelines/
```

## Validating manifests

```bash
claude plugin validate .claude-plugin/marketplace.json
claude plugin validate plugins/family/.claude-plugin/plugin.json
claude plugin validate plugins/technology/.claude-plugin/plugin.json
```
