# HORIZON — Mode d'emploi

Guide opérationnel de mise en ligne, de mise à jour et de personnalisation du site.
Registre : documentation technique. Toutes les commandes sont à exécuter depuis la racine du dossier `horizon/`, sauf indication contraire.

---

## 1. Prérequis

| Élément | Nécessité | Remarque |
|---|---|---|
| Un navigateur web | Toujours | Pour l'aperçu local et la consultation. |
| Un compte GitHub | Pour GitHub Pages | Gratuit ; dépôt **public** requis pour Pages sur le palier gratuit. |
| `git` en ligne de commande | Recommandé | Vérifier : `git --version`. Alternative sans Git : Netlify Drop (§ 4.1). |
| `python3` | Facultatif | Uniquement pour l'aperçu local via serveur (§ 6). |

Aucune installation de dépendances (`npm`, build, etc.) n'est requise : le site est un fichier HTML autonome.

---

## 2. Contenu du dossier

```
horizon/
├── index.html        # le site (HTML + CSS + JavaScript embarqués)
├── README.md         # présentation concise
├── MODE-EMPLOI.md    # ce guide
├── LICENSE           # licence MIT
├── CITATION.cff      # métadonnées de citation
├── .gitignore        # exclusions Git
└── .nojekyll         # désactive le traitement Jekyll sur GitHub Pages
```

> Le fichier `.nojekyll`, vide, est important : il empêche GitHub Pages d'interpréter le dépôt comme un site Jekyll et de masquer d'éventuels fichiers commençant par un tiret bas.

---

## 3. Déploiement sur GitHub Pages (recommandé)

### 3.1 Préparation

Avant tout envoi, remplacer les deux marqueurs `<utilisateur>` par votre identifiant GitHub, dans :
- `README.md` (lien de démonstration et URL du dépôt) ;
- `CITATION.cff` (champ `url`).

### 3.2 Envoi du dépôt

```bash
git init
git add .
git commit -m "HORIZON v1.0 — observatoire de prospective stratégique"
git branch -M main
git remote add origin https://github.com/<utilisateur>/horizon.git
git push -u origin main
```

### 3.3 Activation de Pages

1. Sur GitHub, ouvrir le dépôt → **Settings** → **Pages**.
2. Sous *Build and deployment* → *Source* : **Deploy from a branch**.
3. Branche : **`main`** ; dossier : **`/ (root)`** → **Save**.
4. Patienter ~1 minute. L'URL publique apparaît en haut de la page :
   `https://<utilisateur>.github.io/horizon/`
5. Reporter cette URL dans `README.md` (ligne *Démonstration*) puis committer la correction.

> **Bouton « Cite this repository »** : grâce à `CITATION.cff`, GitHub propose automatiquement un export de citation (APA, BibTeX) sur la page d'accueil du dépôt.

---

## 4. Alternatives d'hébergement

### 4.1 Netlify Drop — sans compte, sans Git (aperçu immédiat)

1. Ouvrir `app.netlify.com/drop`.
2. Glisser-déposer le **dossier** `horizon/` (ou le seul `index.html`).
3. Une URL en `*.netlify.app` est générée sur-le-champ.

Idéal pour valider en direct ; à réserver aux tests, l'URL étant éphémère tant qu'elle n'est pas rattachée à un compte.

### 4.2 Cloudflare Pages — bande passante illimitée

Connecter le dépôt GitHub (aucune commande de build à indiquer, laisser le champ vide), ou téléverser via le CLI **Wrangler**. Recommandé si un trafic élevé est anticipé.

---

## 5. Domaine personnalisé (gratuit)

1. Créer à la racine un fichier nommé `CNAME` (sans extension) contenant **une seule ligne** : votre domaine, p. ex.
   ```
   horizon.exemple.org
   ```
2. Chez votre registraire DNS, ajouter un enregistrement `CNAME` pointant votre sous-domaine vers `<utilisateur>.github.io`.
3. Committer et pousser. Dans **Settings → Pages → Custom domain**, saisir le domaine et cocher **Enforce HTTPS** une fois le certificat émis.

---

## 6. Aperçu local

Ouverture directe : double-cliquer sur `index.html`.
Rendu identique à la production (utile pour tester chemins et polices) :

```bash
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

---

## 7. Mettre à jour le site

Après toute modification de `index.html` :

```bash
git add index.html
git commit -m "Mise à jour du contenu"
git push
```

GitHub Pages redéploie automatiquement en une à deux minutes. Si l'ancienne version persiste, vider le cache du navigateur (rechargement forcé : `Ctrl/Cmd + Maj + R`).

---

## 8. Personnalisation

Tout le contenu et l'apparence résident dans `index.html`. Deux zones distinctes.

### 8.1 Palette et typographie — bloc `:root` (CSS, en haut du fichier)

Les couleurs sont centralisées en variables. Modifier une valeur la propage à tout le site.

| Variable | Rôle |
|---|---|
| `--ink`, `--ink-2`, `--ink-3` | Fonds (du plus sombre au plus clair). |
| `--bone` | Texte principal clair. |
| `--ember` | Accent principal (trajectoire « préférable »). |
| `--horizon` | Accent secondaire (données, « plausible »). |
| `--plum` | Accent tertiaire (« possible », signaux extrêmes). |
| `--serif`, `--sans`, `--mono` | Familles typographiques (Fraunces / IBM Plex Sans / IBM Plex Mono). |

Pour un rendu **hors-ligne** intégral, remplacer l'appel `<link>` aux polices Google par des polices intégrées (base64) ou par des familles système dans ces variables.

### 8.2 Contenu — objets de données (JavaScript, section `DATA`)

Le contenu est piloté par des tableaux ; chaque champ textuel est bilingue au format `{fr:"…", en:"…"}`. Éditer ou ajouter une entrée met à jour le site sans toucher au HTML.

| Objet | Contenu | Pour ajouter une entrée |
|---|---|---|
| `T` | Dictionnaire des libellés d'interface (FR/EN). | Ajouter la même clé dans `fr` **et** `en`. |
| `METHODS` | Les méthodes de prospective. | Copier un bloc `{tag,name,desc,src}`. |
| `DOMAINS` | Les sept domaines et leurs notes par horizon. | Renseigner `conf` et `h` pour **2030, 2040, 2050** ; associer un `icon` défini dans `ICONS`. |
| `AXES` | Les axes d'incertitude de la matrice. | Ajouter `{id,label,pos,neg}` ; l'axe devient sélectionnable. |
| `SIGNALS` | Les signaux faibles. | Le champ `k` doit correspondre à une catégorie existante pour le filtrage. |
| `REFS` | La bibliographie. | Ajouter `{a,t,y}` (auteur, titre, année). |

> **Règle bilingue** : ne jamais laisser un champ `{fr, en}` incomplet. Une clé de `T` manquante dans une langue s'affichera telle quelle (nom brut de la clé).

Les trois horizons (2030 / 2040 / 2050) sont câblés à la fois dans les boutons HTML (section *Horizons*) et dans les clés de `DOMAINS.h`. Pour changer un millésime, modifier les deux.

---

## 9. Dépannage

| Symptôme | Cause probable | Correctif |
|---|---|---|
| Page blanche ou 404 sur Pages | Fichier d'accueil mal nommé | Le fichier doit s'appeler exactement `index.html`, à la racine. |
| Ancienne version affichée | Cache navigateur / CDN | Rechargement forcé (`Ctrl/Cmd + Maj + R`) ; attendre 1–2 min. |
| Polices non chargées | Absence de réseau ou `<link>` bloqué | Vérifier la connexion ; ou intégrer les polices (§ 8.1). |
| Un libellé s'affiche comme `hero.title` | Clé absente dans `T` pour la langue active | Compléter la clé dans `T.fr` **et** `T.en`. |
| La bascule FR/EN ne réagit pas | Erreur JavaScript introduite | Ouvrir la console du navigateur ; contrôler la virgule/accolade de la dernière entrée éditée. |

---

## 10. Sauvegarde et versionnage

Chaque `git push` constitue un point de restauration. Pour publier une version jalonnée :

```bash
git tag -a v1.0 -m "Première édition publique"
git push origin v1.0
```

---

**Assistance Multi IA** · Genève · [Assistant-Multi-AI@proton.me](mailto:Assistant-Multi-AI@proton.me)
