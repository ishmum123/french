# TODO (v2 candidates)

Residuals from the v1 QA rounds. The rules already in place are described
in `README.md` and in `engine/tools/packbuilder/langs/fr.py`.

## Sentence links
- Noun/verb homographs with a noun subject are still read as nouns when the
  tagger says so: "Le Japon produit..." links le produit, "L'heure ...
  approche" links l'approche, "Maîtriser une langue demande..." links la
  demande. The subject-pronoun rule only covers je/tu/il/elle/on/ils/elles.
  "pour déjeuner" (to have lunch) links the noun le déjeuner.
- Object clitics la/les before a verb are sometimes read as articles
  ("je la porte" can link la porte). The verb-after-determiner rule skips a
  determiner that follows a subject or object pronoun, but a clitic after a
  noun subject ("Marie la voit") still follows the tagger.
- Fixed expressions whose noun has another sense are unlinked from a short
  list (bon marché, en général, à part, en conserve, au fait). Others
  still link word by word.
- Noun/verb homographs after a noun subject follow the tagger: "Votre vol
  part à 14 h" links la part.
- "fort au rugby" (good at rugby) links fort with its main gloss "strong".
- A feminine noun after an adjective can be read as the adjective:
  "Les mauvaises nouvelles" links nouveau, not la nouvelle.
- Adjectives used as interjections link the adjective: "Mince !" links
  mince (thin).
- Participle/adjective homographs after a noun follow the tagger:
  "du poisson cru" links croire.
- "être juste" (to be fair) links the adverb juste.
- Gender homographs have one entry per lemma (la poste "post office" has no
  le poste "job" beside it; le tour / la tour, le livre / la livre). A token
  whose determiner shows the other gender links nothing.
- au, aux, du, des link only to the preposition (à, de), not also to the
  article le.
- Fixed expressions not merged: n'importe (quoi), avoir l'air, faire mal,
  en avoir marre (marre is a headword glossed "fed up (en avoir marre)").
  Their parts link word by word. (il y a, est-ce que, excusez-moi, s'il te
  plaît, lors de, à travers, petit déjeuner are phrases since QA round 2.)

## Words and glosses
- The reflexive gate uses 2-7 linked sentences per verb, so it is noisy.
  Reverted verbs show a combined gloss ("occuper: to take up; s'occuper:
  to be busy"). When both halves agree the gloss can read oddly
  ("reposer = to rest; se reposer: to rest").
- A few glosses keep a wordy Wiktionary tail or a secondary sense first
  (concevoir "to design"). Add them to
  `tools/gloss_overrides.json` as they are found.
- Days and months are shown without an article.
- Ids are frozen in `tools/id_map_v1.json`. New words get fresh ids; never
  renumber existing ones.
- Appended se-senses for less common verbs come from Wiktionary's first
  reflexive sense (REFL_SENSE in fr.py holds hand ones for common verbs);
  B1 ones are unreviewed.
- A1/A2 glosses were hand-reviewed in QA round 2 (overrides in
  `tools/gloss_overrides.json`). B1 glosses are ranker output only.

## Verification
- Browser verification of `index.html` (every tab, fr-FR TTS voice, typing
  with accents at each level, gap items, audio) is still to do.
