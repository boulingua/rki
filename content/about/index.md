---
title: About this course
page_type: appendix
author: S. Le Boulanger
description: "What RKI covers and what it deliberately does not: scope, method, the language variety taught, the orthographic conventions, curriculum alignment, materials pipeline and licence."
---

## What this site is

**RKI** — *ру́сский как иностра́нный*, Russian as a foreign language — is a
free, openly licensed course covering the Cyrillic script and CEFR levels A1
to B2. It is written for two audiences at once: teachers of Russian in the
German *Gesamtschule* system who need a curriculum-aligned skeleton they can
teach from, and independent adult learners who want a structured path with
examinations at the end of each level rather than a stream of exercises.

The course assumes nothing. It does not assume the alphabet, it does not
assume a first language other than German or English, and it does not assume
access to a teacher. Every unit is complete as a reading text, and every unit
also ships what a classroom needs: a slide deck, a printable worksheet, an
answer key and audio.

## Scope, and what is not claimed

The course covers **Level 0 (script) and A1 to B2**. C1 and C2 are out of
scope and will stay out of scope. Free material rarely reaches those levels
honestly — the reading load alone is beyond what a single author can source,
write and license — and a course that advertises C1 without it misleads the
learner it exists to serve.

Within B2 the coverage is deliberately partial and the gaps are declared. See
*Curriculum alignment* below.

## The language taught

**Standard Moscow Russian in a contemporary neutral register.** No regional
variety, no heritage-speaker variety, no archaism kept alive by textbooks. The
audio uses two standard voices, one female and one male, so that dialogues
alternate speakers rather than reading as a monologue.

## Orthographic conventions

Four decisions govern every page of teaching text, and they are worth stating
because they differ from what a learner will find in a Russian book.

- **Cyrillic from the first minute.** A light, ISO-9-flavoured transliteration
  runs alongside the Cyrillic through Level 0 and the first A1 units as a
  scaffold, thins out, and is gone by the end of A1. Transliteration that
  outlives its usefulness stops a learner from ever reading.
- **Stress is marked.** Every multisyllabic word in teaching text, in
  worksheets and on slides carries the acute: `хорошо́`, `говори́ть`,
  `понима́ю`. Russian stress is lexical, mobile within a paradigm, and unmarked
  in ordinary print — and it determines vowel quality, since unstressed **о**
  is not [o]. A word printed without its stress is a word a beginner cannot
  pronounce.
- **ё is always ё.** Never е. Russian print conflates them freely; a learner
  who meets `все` where `всё` was meant learns a wrong vowel and a wrong
  stress at the same time, because **ё** is always the stressed syllable and
  therefore never takes an acute.
- **Stress marks are removed where reading is the point.** From B1 the
  authentic reading passages drop the acute, because printed Russian has none
  and a reader who depends on the marks can read only textbooks. Teaching
  text, paradigms and glossaries keep their marks throughout.

## The five-step unit

Every unit follows the same sequence, so that the structure of a lesson is
predictable and the teacher's improvisation goes into the content:

1. **Activate** — recover prior knowledge; an image, a question, a short
   exchange.
2. **Input** — the model text, dialogue or paradigm, with its vocabulary.
3. **Practise** — controlled tasks with answer keys, differentiated for
   support and for extension.
4. **Apply** — the free productive task: writing, speaking, role-play,
   mediation.
5. **Reflect** — self-assessment against the can-do statements the unit
   claims.

Model exams shift the sequence to *task → model → strategy → attempt →
feedback*.

## How the grammar is sequenced

Two features of Russian dominate the syllabus and both are spiralled rather
than front-loaded.

The **six-case system**, crossed with three genders, two numbers and the
animacy distinction, is the largest single load in the language. A1 takes
three cases — nominative, accusative, prepositional — and stops there. A2
completes the paradigm with genitive, dative and instrumental. B1 and B2
return to it in use rather than in tables.

**Verbal aspect** appears at A1 only lexically: pairs learnt as vocabulary, in
fixed phrases, unanalysed. It is introduced properly at A2 alongside the past
tense, where the contrast between process and result is clearest, and revisited
at B2 for the infinitive, the imperative, negation and the general-fact
imperfective. It has no clean German or English analogue and it is never
finished in one unit.

## Curriculum alignment

Units declare CEFR can-do statements in their front matter; each statement
resolves to a descriptor identifier in the shared boulingua curriculum
framework, which is grounded in the CEFR Companion Volume (2020). The course
declares **`core` conformance (A1–B1), with a partial extension into B2**.

`core` means that every in-scope CEFR scale carrying an official A1, A2 or B1
descriptor is implemented in the corresponding level. Where the Companion
Volume provides no descriptor for a (level, scale) cell, the course records
`no-official-descriptor`. This distinction matters: an absent descriptor is
not a failure, whereas a scale silently missing from the course is. The
machine-readable manifest lives in `conformance.yml` in the repository, and it
is what any claim on this site should be checked against.

At B2 the course implements the high-frequency scales — reception, production,
spoken and written interaction, and the core linguistic, sociolinguistic and
pragmatic scales — and declares the remaining mediation and plurilingual
scales as gaps. Level 0 maps to pre-A1 descriptors where they exist and
records its script-literacy objectives as course-local, since the CEFR does
not describe them.

The examinations on this site are **model exams in the format of their level**.
They are written for this course, they are not connected to any examination
board, and passing one certifies nothing.

## Materials and audio

Slide decks and worksheets are produced from the shared branded XeLaTeX
templates and committed as PDFs; the deployment pipeline verifies that they
are present and correctly attributed but never compiles them, so the site does
not depend on a TeX installation. Audio is produced with the shared
Piper-based pipeline. Two caveats are stated on the audio itself rather than
hidden: the synthesiser does not read the combining acute as a stress signal,
so the accent is stripped from its input and the pronunciation rests on the
model's own lexical stress; and free synthesis mis-stresses low-frequency
words often enough that every segment is checked by ear and corrected where
wrong.

## Sources and originality

Texts, dialogues, exercises and examination stimuli are written for this
course. Quoted material is limited to sources in the public domain or under an
open licence, and is cited where it appears. No copyrighted textbook material
is reproduced.

## Licence

- Site code, layouts and scripts: **MIT**.
- Teaching content — units, exams, appendices, worksheets, slide decks:
  **CC BY-SA 4.0**, attributed to S. Le Boulanger.

See [Impressum]({{< relref "/impressum" >}}),
[Datenschutzerklärung]({{< relref "/datenschutz" >}}) and
[Haftungsausschluss]({{< relref "/haftungsausschluss" >}}) for the legal
details, and the [appendices]({{< relref "/appendices" >}}) for the reference
apparatus.
