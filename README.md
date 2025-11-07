# Challenge - Inspection et Analyse d'un Repository GIT

## Consignes générales

Ce challenge a pour but d'évaluer votre capacité à **explorer, comprendre et analyser l'historique d'un projet GIT**.

### Règles

- **Aucune interface graphique n'est autorisée**, vous devez travailler **exclusivement en ligne de commande** (sauf pour le FORK depuis Github)
- **L'utilisation d'outils d'intelligence artificielle est strictement interdite.**
- Vous pouvez utiliser la documentation à l'adresse suivante: https://git-scm.com/book/fr/v2
- **Objectif : comprendre l'évolution du code et reconstituer les décisions prises.**

## Travail à effectuer

Le dépôt d'origine à utiliser est disponible à l'adresse suivante :

```bash
https://github.com/ETML-RRY/324_inspection_git.git
```

### Partie 1 - Préparation

1. Faites un _FORK_ du dépôt sur votre compte GitHub (Attention il faut copier toutes les branches donc il faut **décocher** la case "Copy the main branch only" sur l'interface de Github)
2. Ajoutez votre enseignant comme collaborateur à votre dépôt forké.
3. Vous trouverez une réplique de ces instructions dans le fichier README.md de votre dépôt.
4. Répondez directement aux questions dans le fichier README.md qui est au format **Markdown**
5. Pour chaque points, veuillez noter la ou les commandes `git` utilisées vous permettant de répondre à la question.
6. Pour chaque partie, effectuez au minimum un commit et un push lorsque vous avez complété les réponses de la partie correspondante.

> Le format Markdown: [https://www.markdownguide.org/basic-syntax/](https://www.markdownguide.org/basic-syntax/)

### Partie 2 — Exploration de base

1. Combien de branches existent dans le dépôt ? Citez-les.

```sh
git branch -r
  origin/HEAD -> origin/main
  origin/experiment/dark-mode
  origin/feature/header
  origin/feature/login
  origin/hotfix/typo
  origin/main
```

2. Quels sont les **tags** disponibles ? A quoi correspondent-ils ?

```sh
git tag
v0.1
v0.2

```

3. Quelle est la **branche principale** du projet ?

```sh
main
```

### Partie 3 — Historique et commits

4. Quel est le message du **premier commit** du projet ?

```sh
git log --reverse
commit 4d28bc59eee6c8f52277bf505642a0e8e3595674 (tag: v0.1)
Author: Romain Rosay <romain.rosay@eduvaud.ch>
Date:   Wed Nov 5 22:15:09 2025 +0100

    Initial commit: structure HTML/CSS/JS + README + docs

```

5. Trouvez le commit où une **clé API** a été ajoutée par erreur. Quel est son identifiant (hash court) ?

```sh
git log -G "API"
commit 1b682c91ef14cda333419e2e387a53033ae575a1

git log --oneline
bea2d1a chore(config): AJOUT TEMPORAIRE d'une clé API (à retirer)
```

6. Quel commit a ensuite corrigé cette erreur ?

```sh
1b682c9 chore(config): retire la clé API et documente la bonne pratique
```

7. Trouvez le commit où le **titre de la page d'accueil** a été corrigé.

```sh
git log --grep "titre"
commit 6317c073f7514d580522c90fa1f0f0402066a48f (origin/hotfix/typo)
Author: Romain Rosay <romain.rosay@eduvaud.ch>
Date:   Wed Nov 5 22:15:21 2025 +0100

    hotfix: corrige la typo 'Wolrd' dans le titre

```

8. Quel est le message du commit qui a **ajouté le fichier `CHANGELOG.md`** et quelle commande avez-vous utilisé ?

```sh
$ git log -- docs/CHANGELOG.md
commit ed62890417d8c8fb880e55a2b8933b80b00ea1bd
Author: Romain Rosay <romain.rosay@eduvaud.ch>
Date:   Wed Nov 5 22:15:30 2025 +0100

    docs: ajoute un changelog de base

```

### Partie 4 — Branches et fusions

9. Quelles branches ont été fusionnées dans `main` ?

```sh
 git branch --merged main -r
  origin/HEAD -> origin/main
  origin/feature/header
  origin/feature/login
  origin/hotfix/typo
  origin/main

```

10. Quelle branche **n'a pas été fusionnée** ? Pourquoi, selon vous ?

```sh
 git branch --no-merged main -r
origin/experiment/dark-mode

 C'est une branche experimentale
```

### Partie 5 — Analyse du contenu

11. Quelle est la **différence principale** entre les fichiers `index.html` dans les versions `v0.1` et `v0.2` et quelle commande permet de le voir rapidement ?

```sh
 git diff v0.1 v0.2 -- index.html
diff --git a/index.html b/index.html
index 2019876..60ce2f7 100644
--- a/index.html
+++ b/index.html
@@ -6,6 +6,7 @@
   <link rel="stylesheet" href="style.css">
 </head>
 <body>
+  <header><nav><a href="/">Accueil</a> | <a href="#">Contact</a></nav></header>
   <!-- NOTE HISTORIQUE: ancien slogan modifié plusieurs fois -->
   <h1>Bienvenue sur notre site Wolrd!</h1>
   <p id="tagline">Un site tout simple pour apprendre Git.</p>

```

12. Que contient la branche `feature/login` ?

```sh
git ls-tree --name-only origin/feature/login -r
.gitignore
README.md
config.js
docs/notes.md
index.html
login.html
script.js
style.css

```

13. Dans quelle branche a été ajouté le code pour le **mode sombre** ?

```sh
origin/experiment/dark-mode
```

14. Quelle bonne pratique de sécurité est évoquée dans les commits du fichier `config.js` ?

```sh
Configuration (ne doit PAS contenir de secrets en prod)
```

### Partie 6 — Réflexion

15. Pourquoi est-il important de **taguer** des versions dans un projet ?

```sh

```

16. Que peut-on déduire du style de travail de l'équipe à partir de cet historique GIT ?

```sh

```

Bonne chance, et surtout... **ne vous perdez pas dans le log !** 😉
