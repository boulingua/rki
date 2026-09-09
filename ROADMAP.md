<!-- status-audit-2026-09-09 -->
> ## Status audit — 2026-09-09
>
> **This repository is still a scaffold:** 5 tracked files, no Hugo shell yet, no `content/` pages, no build output committed.
> The build plan below stands and is not superseded. This box records what the platform
> now requires that the plan predates, and what the first moves are.
>
> **Declared scope (from this plan):** A1 → B2, preceded by a Level 0 Cyrillic/script onboarding stage. C1/C2 are out of scope. Level 0 maps to preA1 descriptors where they exist.
>
> ### Platform requirements added since this plan was written
>
> - **`conformance.yml` at the repo root is mandatory** to declare any conformance level.
>   The framework (`curriculum` v1.1.0) defines `core` (A1–B1), `full` (A1–C1) and
>   `complete` (Pre-A1–C2). **No course in the organisation has this file yet** — not even
>   `efl`, which has the descriptor IDs in place. Absence of the manifest, not absence of
>   content, is what currently blocks every conformance claim in the suite.
> - **Descriptor IDs take the form `A1.REC.overall-oral-comprehension.01`.** Every
>   `implements_id` must resolve against `curriculum/levels/`; `conformance_audit.py
>   resolve` is the gate.
> - **Shortcodes, CSS tokens and layout chrome come from the shared `kit` Hugo module.**
>   A course repo holding its own copies is drift.
> - **CI is shared** and lives in `boulingua/.github`: `course-build.yml`,
>   `kit-drift.yml`, `link-check.yml`, `materials-latex.yml`, `org-audit.yml`.
> - **`[taxonomies]` is declared in no course `hugo.toml` today** — including the three
>   mature ones. Declare it here from the start rather than inheriting the omission.
>
> ### First moves, in this order
>
> 1. **Instantiate from `pagegen`.** Copy the template's `hugo.toml`, `go.mod` and CI entry point; do not copy layouts, shortcodes or CSS — those arrive from the shared `kit` module, and a local copy is drift that `kit-drift.yml` will flag.
> 2. **Write `conformance.yml` before the first unit.** Declare `framework: boulingua-curriculum`, `framework_version: 1.1.0`, the target from the scope above, and `conformance_status: in-progress`. Authoring units before the manifest exists is how `daf`, `efl` and `fle` each ended up with descriptor IDs in front matter that no machine can audit.
> 3. **Author unit 01 as a complete vertical slice** — page bundle, exam sibling bundle, slide deck, worksheet, audio and descriptor IDs — and only then scale out. One finished unit settles every convention question the remaining units would otherwise re-open.
>
> ### Where this sits in the suite
>
> Sequencing across all 18 courses, and the reasoning behind the order, live in
> [`boulingua/.github/ROADMAP.md`](https://github.com/boulingua/.github/blob/main/ROADMAP.md).
> The reference implementation to copy from is **`efl`** (180 unit bundles + 180 exam
> bundles, `unitNN-slug` naming, `page_type` and a `curriculum:` block on every unit).

---
# RKI — Russian course roadmap

> Русский как иностранный. Building the entire boulingua Russian course — content and website — from an empty scaffold to a live course on the world map. This roadmap is the working plan; it conforms to the `kit` platform standard, the `curriculum` framework, and the binding VG Wort standard.

## 1. Overview

**What this is.** A free, openly-licensed Russian-as-a-foreign-language course (code `rki`, signature accent `#198D5B` / dark `#7EE7B9`) for the German *Gesamtschule* system and independent adult learners, published as a static Hugo site (hugo-coder) with committed materials and audio, following the boulingua five-step unit model (Activate → Input → Practise → Apply → Reflect).

**Target learners.** German-L1 (and English-comfortable) absolute beginners with no prior Cyrillic; secondary-school pupils and self-studiers who want structured, exam-backed progression with printable worksheets and native-voice audio.

**Realistic CEFR scope.** **A1 → B2**, preceded by a **Level 0 Cyrillic/script onboarding** stage. C1/C2 are explicitly out of scope for this instantiation (free material rarely reaches them honestly). Pre-A1 (CEFR "preA1") descriptors are folded into Level 0 + early A1 where official descriptors exist.

**The 3–5 defining challenges (drive every decision below):**
1. **Cyrillic script.** Learners cannot read anything on day one. Onboarding the alphabet (33 letters, print vs. italic/cursive forms, handwriting) is a prerequisite gate, not an afterthought — hence Level 0.
2. **Six-case system + gender/animacy.** Russian nominal morphology (6 cases × 3 genders × number, plus animacy) is the dominant grammar load and must be spiralled across A1–B2, not front-loaded.
3. **Verbal aspect.** The imperfective/perfective distinction pervades every tense and has no clean German/English analogue; it needs its own recurring treatment.
4. **Free stress + vowel reduction.** Stress is lexical, mobile, and unmarked in normal orthography but changes pronunciation (о→[а], е→[и]). The course must **mark stress** (аку́т) in all teaching text and reflect reduction in audio.
5. **Font + TTS coverage.** Every layer (web font, slide/worksheet LaTeX, TTS) must fully cover Cyrillic including the stress-accent combining diacritic and the letter ё.

## 2. Language & localisation decisions

Each decision is opinionated with a recommendation.

- **Writing system.** Teach in **Cyrillic from Level 0**; use romanization (a light scientific/ISO-9-flavoured transliteration) **only** as a temporary scaffold inside Level 0 and the first A1 units, then drop it. Decision: **Cyrillic-first, transliteration as a fading crutch, gone by A1 end.**
- **Stress marking.** Mark stress with the combining acute (U+0301) on every multisyllabic teaching word in units, worksheets and slides (e.g. `хорошо́`). Keep ё written as ё (never е) in all teaching text. Decision: **stress marks and explicit ё everywhere in didactic text**; drop stress marks only in "authentic-text" reading tasks at B1+ to build real-world reading.
- **Variant/dialect.** **Standard (Moscow) Russian**, contemporary neutral register. No regional or heritage variants. Decision: **standard literary Russian, neutral register.**
- **RTL.** Not applicable — Cyrillic is LTR. No bidi handling needed.
- **Web font (Cyrillic coverage).** **The kit as it stands today would render this course as tofu, and that has to be fixed before unit 1.** Measured from the cmap of the committed file, the kit's `fonts/SourceSans3-Regular.ttf` carries **781 codepoints and zero in U+0400–U+04FF** — no Cyrillic at all; the seven `.woff2` files in the kit's `static/fonts/` are every one of them the `latin_latin-ext` subset of the same face, and the bundled JetBrains Mono is a 405-codepoint subset with no Cyrillic either. What is wrong is the *subsetting*, not the family: full upstream Source Sans 3 **3.052R** measures 1,648 codepoints including **156 Cyrillic** (ё among them), and JetBrains Mono 2.304 carries 122. Decision: **keep the families and replace the subsets** — full upstream Source Sans 3 / JetBrains Mono, self-hosted, with the Cyrillic range subsetted by `build_fonts.py` from the `fonts.yaml` manifest (F3), which declares ranges by codepoint rather than by Google range name. No new typeface is needed for Russian. Keep the visual QA of ё and combining-acute rendering in both themes — U+0301 is present even in the bundled subset, so what needs checking is its *placement over Cyrillic bases*, not its existence.
- **Native-voice / Piper TTS.** Piper publishes four Russian voices, but only two of them are redistributable, and the licence check reverses the obvious choice. `ru_RU-irina-medium` states `License: Unknown` on its model card and therefore **cannot ship** — no statement is not permission — and `ru_RU-ruslan-medium` is **CC BY-NC-SA 4.0**, which cannot go inside a CC BY-SA 4.0 work at all. Decision: **primary `ru_RU-denis-medium`, second voice `ru_RU-dmitri-medium`** — both **CC0**, both medium tier, which still gives the alternating dialogue pair this course wants. Register the pair by adding a row to `kit/audio/voices.yml`, the single source of truth for voice IDs; they are read from that file and are **never hand-typed**, because a transliterated ID is how a 404 gets written into a download script. Caveat: Piper does not read the U+0301 accent as a stress signal — **strip combining accents from the TTS input string** (keep ё) so pronunciation is correct, and rely on the model's own lexical stress; spot-check reduction and stress on a sample and hand-fix segment text where wrong.
- **Level-0 script onboarding.** A dedicated **`content/level-0/`** section (page_type: section) with letter-group units, handwriting/cursive notes, keyboard layout (ЙЦУКЕН) guidance, and a reading-readiness check. Decision: **Level 0 is a first-class section and a hard prerequisite** surfaced in the menu before A1.

## 3. Instantiation from the kit

Stand up the buildable site first; author content second. Nothing shared is copied.

1. **Create the repo around the kit.** `rki/` holds a short `hugo.toml` (baseURL, title, languageCode, `[params]`, menus) whose `[module]` block carries `[[module.imports]] path = "github.com/boulingua/kit"`, a `go.mod`/`go.sum` requiring `github.com/boulingua/kit` at the pinned tag (`v1.0.0`), `boulingua.yml` (the per-course config the gate battery reads), the twelve-line `.github/workflows/deploy.yml` calling the org's reusable workflow, an empty `content/` skeleton with an empty `data/vgwort.yaml`, and the three legal pages — preserving `LICENSE`, `README.md`, and the existing `brand/` icons already present in `rki/`. `layouts/`, `assets/`, `i18n/`, `archetypes/` and `scripts/` are **not** copied and must never appear in this repo: they are the drift surface, and a file that is not here cannot fork. The kit's `data/` arrives with the module as well — this repo's `data/` holds only `vgwort.yaml`. Hugo resolves the shared surface from the module; CI checks the kit out at the pinned tag so `scripts/` and the gate battery are on disk before Hugo runs.
2. **Vendor `_materials/`.** Run `kit materials sync`, which assembles the kit's `latex/`, `fonts/` and `brand/icons/` into the flat tree the LaTeX build expects, and commit it. This is the only vendored surface, because XeLaTeX cannot read a Hugo module; it is hash-gated against `kit.lock`, so a hand-edited file fails the build rather than forking silently. (Earlier drafts said to copy `_materials/` from the template — `pagegen` never had one.)
3. **Edit only the marked `hugo.toml` values (S):**
   - `baseURL = "https://boulingua.github.io/rki/"`
   - `title = "Русский — RKI — S. Le Boulanger"`
   - `languageCode = "ru"`, `defaultContentLanguage = "ru"` (UI chrome stays bilingual DE/EN as the sister sites; content language is Russian)
   - `params.navTitle = "RKI"`, `description`/`keywords` for Russian
   - `params.code = "rki"` (this selects the accent — do **not** edit CSS). Set it: the kit ships the neutral graphite `template` accent as its default, so an unconfigured course looks obviously wrong instead of looking like DaF.
   - `params.plausible.domain = "boulingua.github.io/rki"` (keep the sub-table **last** under `[params]` — the TOML sub-table trap)
   - `[[params.social]]` url → `https://github.com/boulingua/rki`
   - `[[menu.main]]` sections → Level 0, A1, A2, B1, B2, Materials, About, Legal
4. **Confirm accent.** The kit's `data/accents.yaml` already carries `rki` (accent `#198D5B`, hover `#126642`, dark `#7EE7B9`) — verified present. It arrives with the module; no change needed, and no `data/accents.yaml` in this repo.
5. **Regenerate brand.** Run the kit's `brand/make_icon.py` to regenerate the pentagon mark + favicons from the `rki` accent into this repo's `brand/` (icons exist but re-run to guarantee they derive from the current accent pipeline).
6. **Fill legal `⟨…⟩` placeholders** in `impressum.md` / `datenschutz.md` / `haftungsausschluss.md`, including the VG Wort METIS disclosure in Datenschutz.
7. **First green build.** `hugo --minify --gc` locally; verify the gate battery passes on an empty-content build; push and confirm `deploy.yml` builds with `--panicOnWarning` and deploys via **GitHub Pages** (`github-pages` environment). Definition of this milestone: an empty but themed Russian site deploys green.

## 4. Curriculum conformance target

- **Declared level: `core` (A1–B1), with a partial `full` extension into B2.** `core` requires every **in-scope** scale that has an official A1/A2/B1 descriptor to be implemented; B2 will be implemented for the high-frequency scales (reception, production, spoken/written interaction, core linguistic/pragmatic) and **declared as a gap** for the thin scales (much of mediation, all plurilingual) rather than faked.
- **In-scope scales** are the closed set in `curriculum/schema/scale-registry.yml` (REC 13, PROD 12, INT 18, MED 20, PLUR 3, LING 6, SOC 1, PRAG 6; SIGN out of scope, no IDs). For every (LEVEL, SCALE) cell with no CV descriptor, record **`no-official-descriptor`** — absence is never a failure, a silently missing scale is.
- **Mapping plan.** Each unit's front matter uses the `curriculum` block with `framework: cefr`, a `cefr_level`, and `cefr_can_do` statements; each can-do resolves to a descriptor ID `{LEVEL}.{DOMAIN}.{SCALE}.{SEQ}` per `curriculum/docs/id-scheme.md`. Every realization carries a resolvable `implements:` reference to a statement in `curriculum/levels/*.md`.
- **Machine-readable scope/coverage manifest.** Publish `rki/conformance.yml` (modelled on `curriculum/examples/de-a1/`) declaring `framework_version`, `language: ru`, `declared_conformance: core`, and the per-scale × per-level matrix (implemented ID vs `no-official-descriptor`). Every `implements:` must resolve, with correct format and global uniqueness. **Gate.** The reusable workflow `boulingua/.github/.github/workflows/course-build.yml@v1` runs `python .curriculum/scripts/conformance_audit.py resolve --manifest conformance.yml --content content`. `id-audit.sh` audits the framework's *own* level files and **cannot** validate this repo. Do not wire it here.
- **Level 0** maps to `preA1` descriptors where they exist (a handful of REC/INT scales) plus non-CEFR script-literacy objectives recorded as course-local (not CEFR-claimed).

## 5. Content creation plan

Phased by level; effort tags **S / M / L**. Recurring cast and theme thread all levels for continuity: **a student, Аня, arriving in a Russian-speaking city — flatmates, university, work, travel** — so vocabulary and situations recur and spiral.

**Per-level unit counts and acceptance criteria:**

- **Level 0 — Cyrillic onboarding (M).** ~5 units: (1) vowels + easy consonants, (2) "false-friend" letters (В Н Р С У Х), (3) remaining consonants + ь/ъ, (4) print↔cursive/italic + handwriting, (5) reading fluency + keyboard. Plus a script-readiness check (exam-style). *Accept:* a learner can decode any Russian word aloud, type Cyrillic, and knows all 33 letters + ё.
- **A1 (L).** ~10 units. Greetings/introductions, gender & number, present tense, nominative + accusative + prepositional, personal pronouns, numbers/time, family, food/shopping, home, daily routine. Introduce aspect *lexically* (не delve). *Accept:* every in-scope A1 scale with a descriptor is mapped; audio + worksheet + slides committed; A1 exam bundle present.
- **A2 (L).** ~10 units. Past tense + aspect proper, genitive + dative + instrumental (full six-case survey), verbs of motion (intro), possessives, comparatives, directions, health, travel, weather. *Accept:* all six cases covered receptively/productively; aspect pairs taught; A2 exam.
- **B1 (L).** ~12 units. Verbs of motion with prefixes, conditional/subjunctive, participles (recognition), reported speech, complex sentences, work/education, media, opinions, culture. *Accept:* `core` conformance closes here — every in-scope A1–B1 descriptor implemented or `no-official-descriptor`; B1 exam.
- **B2 (M, partial).** ~10 units. Aspect nuance, participles/gerunds (production), abstract topics, register, argumentation, longer authentic reading (stress marks dropped). *Accept:* B2 implemented for high-frequency scales, gaps declared in `conformance.yml`; B2 exam.

**Exams** are first-class sibling bundles (`…-exam/index.md`, `page_type: exam`, shared `unit_nr`), one per level minimum (plus optional per-unit quizzes), with `duration_min`, `total_points`, `notenschluessel`, and a PDF under `static/downloads/<level>/`.

**Appendices (M):** Cyrillic + cursive chart; full case-ending tables (nouns/adjectives/pronouns); aspect-pair glossary; verbs-of-motion table; stress/reduction guide; A1–B2 thematic glossary; common German-L1 error list; assessment grid. Each ≥1800 chars carries a VG Wort mark.

## 6. Website & materials

- **Section landings** (`_index.md`, `page_type: section`) rendered via **shortcodes only** (never raw HTML) — one per Level 0/A1/A2/B1/B2 and the Materials hub.
- **Materials pipeline.** Slide decks and worksheets from the kit's LaTeX templates (`kit/latex/`, Beamer/XeLaTeX and XeLaTeX, vendored into `_materials/`), both compiled locally (twice, for the TikZ watermark) and **committed** under `static/materials/` + `static/downloads/`; CI only verifies presence + attribution (no TeX Live in the deploy path). The print side has the same defect as the web side and the same fix: the kit's bundled `fonts/SourceSans3-*.ttf` carry no Cyrillic (781 codepoints, zero in U+0400–U+04FF), so the F3 rebuild from full upstream Source Sans 3 3.052R is a **precondition** for the first deck, not a QA step after it. Once rebuilt, verify Cyrillic + the stress accent in XeLaTeX (fontspec); if the combining acute still mis-renders in LaTeX, precompose stressed vowels rather than adding a second family.
- **Audio.** Via the kit's Piper pipeline (`kit/audio/`; `ru_RU-denis-medium` + `ru_RU-dmitri-medium`, both CC0 — the licence-clear pair per §2, read from `kit/audio/voices.yml`, never hand-typed), OGG/Opus 48 kbit/s mono, committed under `static/materials/audio/<unit>/`, manifest in `data/audio/<unit>.json`, rendered as accessible `<audio>` players with visible transcripts. **TTS input must strip U+0301 accents, keep ё**; spot-check stress/reduction and hand-fix segment text.
- **Thumbnails** generated by `scripts/render_thumbs.py`; **downloads** verified present + attributed by `scripts/verify_downloads.py`.

## 7. VG Wort — pixel assignment for ALL content pages (required)

Non-negotiable, per `kit/docs/vgwort-standard.md`. **Every** creative content page ≥1800 rendered characters gets exactly **one** VG Wort Zählmarke on exactly **one** URL: every unit, every exam, every appendix, and long-form editorial pages (About / course overview / Level-0 intro prose). **Never** on navigation (home, `/materials/`, tag/category indexes), paginated continuations, or the templated legal pages.

**Process for each work:**
1. Draw fresh **public** codes (32-hex) from the author's VG Wort **T.O.M.** account — never invent, never reuse a code already assigned, never expose the private code.
2. Register each in `data/vgwort.yaml` keyed by `url:` or `path:`, with `public_id`, `pixel_url` (`https://vg09.met.vgwort.de/na/<code>`), `min_chars: 1800`, `author`, `registered_at`.
3. Rendering goes through the single resolver partial `layouts/_partials/vgwort/url.html` → `<head>` preload + eager off-screen `<img>` in body (no JS, no consent gate, `loading="eager"`, `visibility:hidden`/off-screen never `display:none`).
4. Record every code in the **private usage registry** (§8 of the standard) — kept outside the repo — mapping code → Projekt `rki` / Sprache Russian / Niveau / URL.
5. Verified by CI: coverage audit (warning), render verify (blocking, page-level uniqueness), hub guard (blocking — `met.vgwort.de` absent from the materials hub). Exclude `vgwort.de` from link-checkers.

**Estimated total marks needed:** units ≈ 5 (L0) + 10 (A1) + 10 (A2) + 12 (B1) + 10 (B2) = **47**; exams ≈ **6** (one per level + L0 readiness); appendices ≈ **8**; editorial (About, section intros ≥1800 chars) ≈ **4–6**. **≈ 65–67 Zählmarken total** — draw ~70 codes from T.O.M. to leave headroom.

## 8. Milestones & sequencing

1. **M0 — Scaffold live (S).** §3 done: themed empty Russian site deploys green to GitHub Pages. *Dep:* none.
2. **M1 — MVP: Level 0 live (M).** 5 Cyrillic units + readiness check + Level-0 slides/worksheets/audio + their VG Wort marks + `conformance.yml` skeleton passing the §4 conformance gate. *Dep:* M0, the Russian voice row added to `kit/audio/voices.yml`, the F3 Cyrillic font rebuild, LaTeX Cyrillic QA. **First public value.**
3. **M2 — A1 complete (L).** 10 units + A1 exam + appendices started; A1 in-scope descriptors mapped. *Dep:* M1.
4. **M3 — A2 complete (L).** Six-case + aspect fully covered; A2 exam. *Dep:* M2.
5. **M4 — B1 complete → `core` conformance met (L).** Every in-scope A1–B1 descriptor implemented or `no-official-descriptor`; B1 exam; appendices complete. *Dep:* M3.
6. **M5 — B2 partial + polish (M).** B2 units + exam; declared B2 gaps in `conformance.yml`; full audio/materials pass; a11y + Cyrillic-rendering QA in both themes.

**Definition of "done / ready to flip from coming-soon to active on the world map":** Level 0 + A1 fully live (units, exams, worksheets, slides, native-voice audio all committed and rendering), every published editorial page ≥1800 chars carries a registered, render-verified VG Wort mark (coverage audit shows 0 unregistered), `conformance.yml` passes the §4 conformance gate with an honestly declared level, all CI gates green, legal placeholders filled, and the site deploys to GitHub Pages. Practically: **flip at end of M2 (A1 live)**; continue A2–B2 as ongoing releases.

## 9. Open decisions & risks (language-specific)

- **Cyrillic font coverage (now a blocker, not a risk).** The committed Source Sans 3 and JetBrains Mono subsets contain **no Cyrillic**, so nothing in this course renders until the F3 rebuild lands. *Mitigation:* treat the rebuild as an M0/M1 dependency; verify with a page of Russian, not with a Latin smoke test.
- **Stress-accent rendering.** Once the rebuilt face carries Cyrillic, the U+0301 combining acute must still sit correctly over Cyrillic bases in both themes **and** in XeLaTeX (slides/worksheets). *Risk:* dotted/clipped glyphs. *Mitigation:* early rendering QA on ё + stressed vowels; precompose if needed.
- **Piper stress accuracy.** Licence and availability are settled — `denis` and `dmitri` are both CC0 — so this is a quality question only. TTS may mis-stress low-frequency words even with accents stripped. *Mitigation:* per-segment listening QA; hand-edit segment text (respell) where wrong; accept as a known limitation of free TTS, documented on the audio page.
- **Transliteration fade-out.** Deciding exactly when romanization disappears (end of Level 0 vs mid-A1) affects learner comfort vs. immersion. *Decision pending pilot;* default: gone by A1 end.
- **Cyrillic keyboard guidance.** How much to teach ЙЦУКЕН vs. phonetic layouts for German-keyboard learners. *Default:* show both, recommend the OS phonetic layout for beginners.
- **Bildungsplan vs CEFR framing.** Whether to also emit `framework: bildungsplan-bw` codes for the Gesamtschule audience (as EFL/FLE do) or stay CEFR-only. *Default:* CEFR-only (like DaF); revisit if a Baden-Württemberg Russian syllabus mapping is requested.
- **Mediation/plurilingual thinness.** These scales are hard to source freely for Russian. *Decision:* declare gaps honestly in `conformance.yml` rather than pad — per the framework's "declare the gap" principle.
