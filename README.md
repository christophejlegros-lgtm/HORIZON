# HORIZON — Observatoire de prospective stratégique

> \*\*Penser les futurs \*plausibles\*, non prédire l'avenir.\*\*
> \*Thinking\* plausible \*futures, not predicting what comes.\*

Site web autonome et bilingue (FR/EN) consacré à la prospective stratégique : épistémologie de l'incertitude, méthodes éprouvées, mégatendances par horizon et matrice de scénarios. **Un seul fichier HTML**, sans build ni dépendance serveur.

A self-contained, bilingual (FR/EN) website on strategic foresight. **A single HTML file**, no build step, no server dependency.

**Démonstration · Live demo →** `https://christophejlegros-lgtm.github.io/horizon/`

\---

## Caractéristiques · Features

* *Cône des futurs* animé — taxonomie probable / plausible / possible / préférable (d'après Voros).
* Bascule bilingue FR/EN sans rechargement.
* Neuf méthodes sourcées, sept domaines × trois horizons (2030/2040/2050), matrice de scénarios 2×2 interactive, veille de signaux faibles.
* Accessible (navigation clavier, `prefers-reduced-motion`), responsive, sans cadre JavaScript.

Seule dépendance externe : les polices Google (Fraunces, IBM Plex Sans/Mono).

\---

## Contenu du dépôt · Repository contents

```
horizon/
├── index.html        # le site complet (HTML + CSS + JS embarqués)
├── README.md         # ce fichier
├── MODE-EMPLOI.md    # guide de déploiement, mise à jour et personnalisation
├── LICENSE           # MIT (adaptable)
├── CITATION.cff      # métadonnées de citation (bouton « Cite this repository »)
├── .gitignore
└── .nojekyll         # désactive Jekyll sur GitHub Pages
```

\---

## Mise en ligne express · Quick deploy

```bash
git init \&\& git add . \&\& git commit -m "HORIZON v1.0"
git branch -M main
git remote add origin https://github.com/christophejlegros-lgtm/horizon.git
git push -u origin main
```

Puis **Settings → Pages** → branche `main`, dossier `/ (root)`.
**Procédure détaillée, alternatives, mise à jour et personnalisation : voir** [**`MODE-EMPLOI.md`**](MODE-EMPLOI.md)**.**

\---

## Licence \& contact · License \& contact

Sous licence **MIT** (voir [`LICENSE`](LICENSE)).
**Assistance Multi IA** · Genève · [Assistant-Multi-AI@proton.me](mailto:Assistant-Multi-AI@proton.me)

<sub>Édition prospective — 2026. Cet observatoire explore des futurs plausibles à fin d'aide à la décision ; il ne prédit pas l'avenir.</sub>

