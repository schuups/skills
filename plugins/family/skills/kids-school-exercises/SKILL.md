---
name: kids-school-exercises
description: 'Generates printable exercise sheets for Quentin (4th grade, Zurich public school) to prepare for tests and strengthen schoolwork. Use this skill when the parent mentions an upcoming test, asks for practice exercises on a school subject, provides a photo of a graded test to create corrective exercises, or has a photo of Quentin''s completed sheet to correct. Subjects: Mathematik, Deutsch, Englisch, Natur Mensch Gesellschaft (NMG), and other 4th grade Zurich subjects. All output in Hochdeutsch (except English exercises). Sheets formatted for printing and completing on paper. Also trigger when the parent shares a teacher semester goals PDF, says Uebungsblatt, mentions upcoming school tests, or uploads any test or completed worksheet.'
---

# Kids School Exercises

Generates structured, printable exercise sheets for Quentin (born 2016, 4th grade Zurich). Sheets are completed on paper; photos of completed sheets can be submitted for correction in a separate session.

**Language rule:** All communication with the parent is in English. All content on the sheet addressed to Quentin is in Hochdeutsch.

**Curriculum basis:** Lehrplan 21 (Kanton Zürich), Zyklus 2 (grades 3–6). Orientation point at end of 4th grade. See Subject Guidelines for competency areas per subject.

---

## Quentin's School Profile

**Born:** 2016 — derive current age from today's date. If 11 or older, flag that the 4th-grade calibration may need updating.

**School:** Public primary school, Zurich, German instruction (Hochdeutsch).

**Key traits relevant to exercises:**
- Rushes into problems without first reading the method — the method box must always precede exercises
- Does not naturally show intermediate steps — scaffolding required; bare answers are never acceptable
- German articles (der/die/das), plural forms, and cases need constant reinforcement
- Benefits most from error-explanation tasks: explaining what was wrong cements understanding more than just correcting
- Responds well to challenge — include at least one harder exercise per session
- Needs to develop internal quality standards — the correction rubric explicitly assesses tidiness and method, not just correct answers

Full developmental and character profile: see `kids-contents` skill.

---

## Semester Goals (Teacher PDF)

At any point the parent may share a PDF of the semester goals communicated by the teacher. When this happens:

1. **Extract and summarise:** list the stated goals per subject and any indicated timeline (e.g. "fractions by mid-semester", "Aufsatz types by end of term")
2. **Prioritise the session plan:** use the semester goals to weight which topics to focus on. If a test is approaching for a topic that appears in the semester goals, treat it as high priority
3. **Flag gaps:** if a goal mentions a topic not yet covered in any previous session described by the parent, surface it in English: "The semester goals mention [topic] — should we prioritise this?"
4. **Update context:** keep the semester goals active in the current session so exercise choices align with what the teacher has indicated matters

If no PDF has been shared and the parent hasn't mentioned semester goals, ask once per new subject area: "Has the teacher shared semester goals or a topic plan for [subject]?"

---

## Mode Identification

| Mode | Trigger | Action |
|------|---------|--------|
| **A — Generate from topic** | Parent gives subject + topic or mentions upcoming test | Generate a full 30-minute session sheet |
| **B — Analyse test photo** | Parent provides photo of a graded school test | Identify errors and patterns, generate targeted corrective session |
| **C — Correct completed sheet** | Parent provides photo of Quentin's filled-in exercise sheet | Assess and correct each exercise on three dimensions |

If the mode is unclear, ask one question before proceeding.

---

## Language Rules

Every word Quentin reads on the sheet is in **Hochdeutsch** — instructions, exercise prompts, method boxes, section headers, example answers. No Swiss German, no abbreviations.

**Exception:** English exercises may be in English. Section headers (e.g. "Warm-up") may remain in Hochdeutsch.

**Strictness — non-negotiable in all model answers and examples:**
- German nouns always carry their article: die Katze, der Hund, das Kind — never omit
- Plural forms always explicitly correct
- Every sentence ends with correct punctuation
- Writing style: complete sentences — never telegraphic

**Tidiness on the sheet:**
- All answer lines at the same left indent
- Exercise numbers formatted identically throughout
- Uniform spacing between exercises
- Never crowd exercises — if an exercise needs 5 lines, give it 5 lines

---

## Session Structure (30 minutes)

| Block | Time | Purpose |
|-------|------|---------|
| **Warm-up** | 5 min | 3–5 quick exercises to activate prior knowledge |
| **Hauptteil** | 20 min | 4–6 exercises from simple to complex; always includes ≥1 Fehleranalyse exercise |
| **Herausforderung** | 5 min | One genuinely harder exercise requiring method + original thinking |

Total: 8–12 exercises depending on subject and complexity.

---

## Print Format

Generate a self-contained HTML file. Do not generate Markdown. The HTML must print cleanly to PDF from a browser without any manual adjustments.

**Required CSS rules — include verbatim in `<style>`:**

```css
@page { margin: 2cm 2.5cm; }
body { font-family: Arial, sans-serif; font-size: 12pt; line-height: 1.6; color: #111; }
h1 { font-size: 14pt; margin-bottom: 0.3em; }
.meta { margin-bottom: 1.8em; }
.meta span { border-bottom: 1px solid #444; display: inline-block; min-width: 10em; }
.hint { border-left: 3px solid #999; padding: 0.3em 0.8em; margin: 0 0 1.8em;
        font-style: italic; color: #555; page-break-inside: avoid; }
.section { font-weight: bold; border-bottom: 1.5px solid #333; margin: 1.6em 0 0.9em;
           padding-bottom: 0.2em; page-break-after: avoid; }
.exercise { margin-bottom: 1.6em; page-break-inside: avoid; }
.ex-text  { margin-bottom: 0.5em; }
.line     { border-bottom: 1px solid #bbb; min-height: 1.9em; margin: 0.35em 0;
            width: 100%; display: block; box-sizing: border-box; }
.fehler   { background: #f5f5f5; border: 1px solid #ccc; padding: 0.6em 1em;
            page-break-inside: avoid; margin-bottom: 1.6em; }
```

**Layout rules — do not deviate:**
- Every exercise is wrapped in `<div class="exercise">` — this prevents exercises from splitting across pages
- Answer spaces are `<div class="line"></div>` elements — full-width, never table cells or columns
- Section headers have `page-break-after: avoid` — they never appear alone at the bottom of a page
- Use 1 `.line` for warm-up answers, 3–4 for Hauptteil, 5–6 for the challenge
- Never use a two-column layout for exercise content

**Sheet structure:**

```html
<!DOCTYPE html><html lang="de"><head><meta charset="UTF-8">
<style>/* paste CSS above */</style></head><body>

<h1>[Fach] – [Thema]</h1>
<div class="meta">
  Name: <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
  &nbsp;&nbsp;&nbsp;
  Datum: <span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
</div>

<div class="hint">💡 [Denkanstoß — see below]</div>

<div class="section">Warm-up (ca. 5 Minuten)</div>

<div class="exercise">
  <div class="ex-text"><strong>Aufgabe 1</strong><br>[text]</div>
  <div class="line"></div>
</div>

<div class="section">Hauptteil (ca. 20 Minuten)</div>

<div class="exercise">
  <div class="ex-text"><strong>Aufgabe N</strong><br>[text]</div>
  <div class="line"></div><div class="line"></div><div class="line"></div>
</div>

<!-- Fehleranalyse: use <div class="fehler"> -->

<div class="section">Herausforderung (ca. 5 Minuten)</div>

<div class="exercise">
  <div class="ex-text"><strong>Aufgabe N</strong><br>[text]</div>
  <div class="line"></div><div class="line"></div><div class="line"></div>
  <div class="line"></div><div class="line"></div>
</div>

</body></html>
```

---

## Denkanstoß (replaces step-by-step Methode)

Include one **Denkanstoß** per sheet — a single question in Hochdeutsch that nudges Quentin toward the right kind of thinking without revealing the method or the steps. The aha! moment must come from him.

**Rules:** one sentence, a question not a procedure, does not name the method or its steps.

**Examples:**
- Written multiplication: *Was kannst du berechnen, wenn du eine Zahl immer wieder addierst?*
- Written division: *Was ist das Gegenteil von Multiplizieren?*
- Word problem: *Was weisst du? Was suchst du?*
- German articles: *Welche Frage stellst du, um den Artikel herauszufinden?*
- Sentence construction: *Wie viele verschiedene Ideen stecken in diesem Satz?*

---

## Fehleranalyse Format

Include at least one in every Hauptteil. Explaining the error beats correcting it — understanding the rule prevents recurrence.

```
**Aufgabe N – Fehleranalyse**

In einer Übung wurde folgende Antwort gegeben:

  ✗  Falsch:  [wrong answer, exactly as written]
  ✓  Richtig: [correct answer]

Erkläre in einem vollständigen Satz, warum die erste Antwort falsch ist:

_____________________________________________
_____________________________________________
```

A correct answer without explanation is not full credit.

---

## Mode A: Generate from Topic

1. Identify subject, topic, and any constraints (upcoming test date, semester goals, specific weak areas)
2. Check if semester goals have been shared — if yes, align exercise selection
3. Design the three-block session appropriate to the subject and topic
4. Generate the exercise HTML file
5. Spawn a verification agent (see **Verification Agent** section below)
6. After the sheet, add a brief note to the parent in English (not part of the printable sheet): what the session targets and a suggested topic for the next session

---

## Mode B: Test Photo Analysis

**Step 1 — Read the test:** identify subject, every question, every answer, every mark lost.

**Step 2 — Diagnose patterns** (not just individual errors):
- Correct calculation, missing steps → method-skipping habit
- Right answer, wrong article → automatism not yet formed
- Word problem with bare number, no unit, no sentence → doesn't know the expected answer format
- Consistent errors on one concept, scattered correct elsewhere → specific knowledge gap
- Correct once, wrong once on same type → inconsistency, needs consolidation

**Step 3 — Generate a targeted session:**
- Warm-up: start from solid ground, approaching the weak area from below
- Main: exercises targeting the specific gaps; at least 2 Fehleranalyse exercises using the actual errors from the test
- Challenge: a variation of the question type that cost marks

Open the sheet with: *"Dieses Übungsblatt basiert auf deiner letzten Prüfung. Wir üben genau das, was noch nicht geklappt hat."*

**Step 4 — Spawn a verification agent** (see **Verification Agent** section below).

---

## Verification Agent

After generating any exercise sheet, spawn a subagent to solve every exercise. This validates that each exercise is solvable as written and produces a reference answer key.

Subagent prompt:
> Read the exercise HTML at [path]. Solve every exercise fully and correctly. For Maths show all intermediate steps. For language exercises provide the complete correct answer with articles and punctuation. For Fehleranalyse write the full model explanation sentence. If any exercise is ambiguous, unsolvable, or inconsistent with Quentin's level, flag it clearly. Save the solutions as [path-solutions.html] using the same HTML/CSS structure with answers in `<div style="color:#060">`.

If the verification agent flags a problem with an exercise, revise it before delivering anything to the parent.

---

## Mode C: Correct Completed Sheet

Assess every exercise on four dimensions:

| Dimension | What it checks |
|-----------|---------------|
| **Richtigkeit** | Is the answer correct? |
| **Methode** | Were intermediate steps shown and the right approach used? A correct answer without working is noted. |
| **Darstellung** | Legible, aligned, tidy? |
| **Sprache** | Grammar, punctuation, and sentence structure — see rules below |

**Sprache / Stil / Präzision — apply to all written answers:**

*Grammar and punctuation:*
- **Satzende:** every sentence must close with a Punkt, Fragezeichen, or Ausrufezeichen. Missing end punctuation is always flagged.
- **Satzanfang:** every sentence begins with a capital letter.
- **Satzlänge:** Quentin's known habit is to write everything in one long sentence without breaks. Any answer containing multiple ideas or clauses that should be separate sentences must be flagged explicitly: *"Dieser Satz enthält mehrere Ideen — bitte in [N] Sätze aufteilen."*
- **Komma:** flag missing commas before subordinate clauses (*weil, dass, wenn, obwohl, der/die/das* as relative pronouns) and between list items.
- **Vollständigkeit:** answers must be complete sentences with subject and predicate where the exercise requires it.

*Writing style:*
- **Lesbarkeit:** answers must be easy to read at first pass. Flag sentences that are convoluted, inverted without reason, or require re-reading to understand.
- **Ordnung:** handwritten answers must be legible and organised. Words must not run together; lines must be respected.

*Precision:*
- **Einheiten:** a numeric answer without its unit is wrong when the exercise involves a quantity (time, weight, length, money, etc.). "45" is not an acceptable answer to a question asking for minutes — "45 Minuten" is. Flag as ✗, not ≈.
- **Vollständige Antwort:** for word problems, a bare calculation result is not a full answer. The answer must be a complete sentence stating what was asked: *"Es dauert 45 Minuten."*

Format per exercise:
```
Aufgabe [N]
- Richtigkeit:   ✓ / ✗ / ≈ (teilweise richtig)
- Methode:       gezeigt / nicht gezeigt / unvollständig
- Darstellung:   ordentlich / unordentlich / unleserlich
- Sprache:       korrekt / [specific issue, e.g. "kein Punkt am Satzende", "fehlendes Komma vor 'weil'", "alles in einem Satz — bitte in 3 Sätze aufteilen"]
- Kommentar:     [What was right, what was wrong, what to fix]
```

End with a summary in English for the parent:
```
What went well: [specific]
To work on:     [max 3 points, specific and actionable]
Next session:   [suggested focus]
```

Recurring errors: flag with *"Dieser Fehler ist bereits einmal aufgetreten."*

---

## Subject Guidelines

### Mathematik — Lehrplan 21 Kompetenzbereich

**Zahl und Variable (Arithmetik)**
- Numbers up to 1,000,000: place value, reading, writing, ordering, rounding (to 10, 100, 1000, 10000)
- Written addition and subtraction: multi-digit, with carrying/borrowing
- Written multiplication: multi-digit × 1-digit; multi-digit × multi-digit (introduced in 4th grade)
- Written division: multi-digit ÷ 1-digit with remainder
- Mental arithmetic (Kopfrechnen): doubling, halving, times tables (1–10), derived facts
- Fractions (introduction): halves, thirds, quarters, eighths — naming, comparing, simple addition of same-denominator fractions
- Times tables: all tables 1–10, fluent recall

**Form und Raum (Geometrie)**
- 2D shapes: triangles (Dreieck), quadrilaterals (Viereck), rectangles (Rechteck), squares (Quadrat), rhombus (Raute), trapezoid (Trapez), parallelogram
- Properties: sides, angles, symmetry axes (Symmetrieachsen)
- Perimeter (Umfang) of polygons
- Area (Flächeninhalt) of rectangles and squares (length × width)
- 3D solids: cube (Würfel), cuboid (Quader), cylinder, cone, pyramid, sphere — naming and properties
- Angles: acute (spitz), right (rechts), obtuse (stumpf)

**Grössen, Funktionen, Daten und Zufall (Sachrechnen/Grössen)**
- Length: mm, cm, dm, m, km — conversion and calculation
- Weight: g, kg, t — conversion and calculation
- Volume: ml, dl, l — conversion and calculation
- Time: seconds, minutes, hours, days, weeks, months, years; calculating durations
- Money: Rappen, Franken — calculating with CHF amounts
- Word problems (Textaufgaben): must follow the three-step format:
  - *Gegeben:* what do we know?
  - *Gesucht / Rechnung:* what do we calculate? (show all steps)
  - *Antwort:* full sentence with correct unit — a bare number without unit is always wrong

**Exercise guidelines:**
- The Denkanstoß (not a step-by-step method) precedes every exercise set — see Denkanstoß section
- Intermediate steps required; bare answers earn a correction note
- Warm-ups: Kopfrechnen — 3–5 fast problems, one per line, no working needed

---

### Deutsch — Lehrplan 21 Kompetenzbereiche

**Sprache im Fokus (Grammar — highest priority for exercises)**
- Wortarten: Nomen (noun + article + plural + case), Verb (conjugation in all persons, Präsens/Perfekt/Präteritum), Adjektiv (agreement with noun), Pronomen (personal, possessive), Artikel, Präposition, Konjunktion, Adverb
- Satzglieder: Subjekt, Prädikat, Akkusativobjekt, Dativobjekt, Adverbiale (of time, place, manner)
- Kasus: Nominativ, Akkusativ, Dativ — recognition and production (not Genitiv at this stage)
- Rechtschreibung rules: ie vs. ei, ss vs. ß (in Swiss German schools: always ss), Groß-/Kleinschreibung, Wörter mit silent h, doubling of consonants
- Zeichensetzung: Punkt, Fragezeichen, Ausrufezeichen, Komma in list and subordinate clauses

**Lesen / Leseverstehen**
- Short text (5–10 sentences) followed by comprehension questions
- Questions should require: recall (literal), inference (reading between the lines), and personal response

**Schreiben**
- Aufsatz types: Erlebnisaufsatz (personal narrative), Beschreibung (descriptive), Anleitung (instructional)
- Key criteria: introduction–body–conclusion structure, varied sentence beginnings, correct punctuation

**Exercise guidelines:**
- Artikelprobe (article + plural) in nearly every warm-up: "der/die/das [Nomen] — Plural: ___"
- Transformation exercises > fill-in-the-blank: "Schreibe den Satz im Plural", "Setze den Satz in den Dativ", "Ersetze das Nomen durch ein Pronomen"
- Fehleranalyse is especially powerful for grammar: the rule-based nature makes explanations specific and checkable
- Spelling: write from memory, then check — never copy exercises

---

### Englisch — Lehrplan 21 (CEFR target: A1–A2 by end of Zyklus 2)

**Vocabulary topics:** school/classroom, family members, food and drink, animals, house and rooms, the body, clothes, weather and seasons, hobbies and sports, time and dates, numbers 1–1000, colors, size/character adjectives

**Grammar:**
- to be: all persons, present and past, questions and negations
- to have: all persons, questions and negations
- Simple present: all persons (+ s/es for 3rd person singular), questions (do/does), negations
- Present continuous: am/is/are + -ing
- Simple past: was/were; regular verbs (-ed); key irregular verbs (go/went, have/had, see/saw, come/came)
- Question types: yes/no (Do you...? Is she...?), wh-questions (What, Where, When, Who, How)
- Pronouns: personal (I, you, he, she, it, we, they), possessive (my, your, his, her)
- Prepositions of place: in, on, under, next to, behind, in front of

**Exercise guidelines:**
- Exercises may be in English or Hochdeutsch — match the format of the test if a test photo was provided
- Vocabulary: always contextual — in a sentence, dialogue, or short text
- Grammar: focus on correct usage in meaningful sentences, not abstract labelling
- Short writing tasks: dialogues, short descriptions (5–7 sentences)

---

### Natur, Mensch, Gesellschaft (NMG) — Lehrplan 21

NMG integrates natural science, social science, history, geography, and civic education. The 12 competency areas are grouped below by typical 4th-grade content emphasis.

**Science (NMG 2, 3, 4)**
- Biology: plants and animals — structure, adaptation, ecosystems, life cycles; habitats (Lebensräume: Wald, Wiese, Gewässer)
- Physics/phenomena: states of matter (solid, liquid, gas); energy forms (light, heat, movement); magnetism; electricity basics
- Human body: organs and their functions; healthy lifestyle; senses

**Geography (NMG 8, 7)**
- Switzerland: 26 cantons and their capitals, major rivers (Rhein, Aare, Rhone, Inn, Reuss, Limmat, Thur), major lakes (Bodensee, Zürichsee, Vierwaldstättersee, Genfersee, Neuenburgersee), major mountains (Gotthard, Jungfrau, Matterhorn), regions (Mittelland, Jura, Alpen, Voralpen)
- Map reading: compass points (N/S/O/W), scale, symbols
- Living environments: comparing urban/rural, Swiss regions

**History (NMG 9)**
- Concept of time: decades, centuries, millennia, timelines, BC/AD
- Swiss history milestones: Rütlischwur (1291), Confederation, key figures
- Interpreting historical sources and images

**Civic education (NMG 10, 6)**
- Switzerland's political system: Bundesrat, Nationalrat, Ständerat, direct democracy
- Community rules, rights and responsibilities
- Production and consumption: where do goods come from?

**Exercise guidelines:**
- Exercises are typically short-answer comprehension, diagram labelling, timeline ordering, or map tasks
- Connect to Quentin's science interests where the topic allows (NMG 3 and 4 especially)
- For history and civics, Fehleranalyse works well: "Diese Aussage über die Schweiz ist falsch — erkläre warum"

---

## Quality Checklist

Before delivering the sheet:
- [ ] All Quentin-facing text in Hochdeutsch (except English exercises)
- [ ] All communication to the parent is in English
- [ ] Every noun in model answers has the correct article
- [ ] Every plural form is correct
- [ ] Denkanstoß present — one guiding question, not a step-by-step procedure
- [ ] At least one Fehleranalyse exercise in the Hauptteil
- [ ] Herausforderung is genuinely harder than the Hauptteil
- [ ] Every exercise wrapped in `<div class="exercise">` with `page-break-inside: avoid`
- [ ] Answer areas are full-width `.line` divs — no table cells, no narrow columns
- [ ] Answer areas sized correctly: 1 line warm-up, 3–4 lines Hauptteil, 5–6 lines challenge
- [ ] Verification agent spawned and solutions file generated
- [ ] Session fits 30 minutes (not overloaded)
