# GUIDELINES.md — Studio Mathieu
*Principes fondamentaux issus de la recherche sur 400+ sources.*
*Ces principes guident toutes les décisions, tous les projets.*

---

## 1. Tu es architecte d'intention, pas codeur

Ton job n'est pas d'écrire du code — c'est de décrire le problème avec précision.
La qualité de ta description détermine la qualité de ce qui est généré.

> "The skill isn't coding. It's describing friction." — Kris Puckett, Stripe

En pratique :
- Avant de demander quoi que ce soit à Claude → formuler le problème en 1 phrase claire
- Si tu ne peux pas expliquer ce que tu veux en termes simples → tu n'es pas prêt à builder
- Le brief est le vrai travail de design

---

## 2. La dérive visuelle est l'ennemi numéro un

Sans contraintes explicites, l'AI prend 200-300 micro-décisions visuelles par session.
À la session 10, ton produit ressemble à 3 produits différents.

La solution : le design system comme **ensemble fermé**.
L'AI choisit dans une liste définie — elle n'invente jamais.

En pratique :
- Zéro décision visuelle laissée à Claude sans token correspondant dans Figma
- Si un token manque dans le design system → le créer dans Figma d'abord, pas dans le code
- Figma est toujours en avance sur le code, jamais l'inverse

---

## 3. Prototyper coûte zéro — la recherche d'abord est obsolète

La logique classique "front-load la recherche avant de builder" ne tient plus.
Avec l'AI, un prototype fonctionnel se génère en minutes.

> "En 2005, faire les choses était cher. Cette logique est cassée." — Jeff Humble

En pratique :
- Valider avec un prototype fonctionnel, pas des wireframes statiques
- Montrer à 10 utilisateurs cibles — 8/10 voient la valeur = validé
- Thin slices > broad MVPs : une expérience complète pour UN cas précis

---

## 4. La mémoire est dans les fichiers, jamais dans l'AI

L'AI n'a aucune mémoire entre les sessions. Ce qui n'est pas écrit est perdu.
Chaque décision, chaque pattern, chaque exception doit être documenté.

En pratique :
- Toute décision importante → Decision-Log immédiatement
- Tout nouveau pattern découvert → CLAUDE.md mis à jour en fin de session
- Si Claude doit re-apprendre quelque chose → c'est qu'on a raté une documentation

---

## 5. Une conversation = une tâche atomique

Les designers qui réussissent avec l'AI travaillent en sessions courtes et ciblées.
Les conversations longues et multi-sujets produisent de l'incohérence.

En pratique :
- Définir la tâche avant d'ouvrir une conversation
- Si le sujet dérive → nouvelle conversation
- Fenêtre de tokens : rester sous 60%, le contexte vient des fichiers pas du chat

---

## 6. Figma est la source de vérité universelle

Ce qui existe dans Figma doit exister identiquement dans le code.
Ce qui existe dans le code doit avoir une origine dans Figma.

En pratique :
- Toujours lire le frame Figma via MCP avant de générer un composant
- Nommer les layers Figma de façon sémantique — c'est le nom du composant
- Un composant non documenté dans Figma n'existe pas encore

---

## 7. Comprendre suffisamment, pas tout comprendre

Tu n'as pas besoin de savoir coder pour contrôler une codebase.
Tu as besoin de savoir poser les bonnes questions et détecter les signaux d'alerte.

Signaux d'alerte à reconnaître :
- Claude génère sans expliquer → demander une explication en 1 phrase
- Un fichier dépasse 100 lignes → questionner la complexité
- La même chose est faite de deux façons différentes → signaler l'incohérence
- Claude propose d'ajouter une dépendance → toujours demander pourquoi

---

## 8. Itérer vite, supprimer agressivement

L'AI rend trivial d'ajouter des features. Le vrai skill est de savoir quoi enlever.
Chaque feature inutile est du contexte en moins pour l'AI, de la complexité en plus.

En pratique :
- YAGNI : ne construire que ce qui est nécessaire aujourd'hui
- Audit mensuel de la codebase : supprimer avant d'ajouter
- Un produit simple qui marche > un produit complexe qui dérive

---

## 9. Le workflow est le produit

Le système qu'on construit (Obsidian + Claude + Figma + GitHub) est lui-même
un produit à maintenir, améliorer, et documenter.

En pratique :
- Studio-Workflow est un projet à part entière avec sa propre roadmap
- Chaque friction dans le workflow → noter dans Studio-Workflow/Changelog.md
- Les bonnes pratiques découvertes en travaillant → mettre à jour ce fichier
