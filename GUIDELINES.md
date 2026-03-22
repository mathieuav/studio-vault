# GUIDELINES.md — Studio Mathieu
*Source de vérité transversale. S'applique à tous les projets.*
*Claude lit ce fichier en priorité avant tout CLAUDE.md de projet.*

---

## 0. Principes fondamentaux

Ces principes ne sont jamais négociés, quel que soit le projet :

- **KISS** — la solution la plus simple qui fonctionne. Toujours.
- **YAGNI** — ne pas construire ce qui n'est pas demandé aujourd'hui.
- **Lean** — valider avant de construire. Prototyper avant de coder.
- **Une tâche = une conversation** — ne jamais mélanger les sujets.
- **La mémoire est dans les fichiers** — jamais dans le contexte de chat.
- **Pas de décision silencieuse** — Claude signale tout choix technique non évident.

---

## 1. Règles de code — non négociables

### Tokens et valeurs
- Zéro valeur brute dans le code (#ffffff, 16px, 8px...)
- Toujours utiliser les tokens CSS définis dans le CLAUDE.md du projet
- Si un token manque → le signaler, ne pas inventer

### Composants
- Un composant = un fichier
- Toujours typer les props (TypeScript)
- Nommer selon le design system Figma (data-name des layers)
- Variantes et états = props explicites, jamais de CSS conditionnel opaque

### Taille et complexité
- Fonctions : 30 lignes maximum
- Composants : 100 lignes maximum
- Si ça dépasse → découper, signaler à Mathieu

### Nommage
- Semantic et greppable : chaque concept a UN nom dans tout le projet
- Pas d'abréviations non évidentes
- Sentence case pour les labels UI, PascalCase pour les composants

---

## 2. Workflow de session

### Ouverture
1. Lire GUIDELINES.md (ce fichier)
2. Lire le CLAUDE.md du projet concerné
3. Résumer en 3 phrases : où on en est, ce qui est bloqué, ce qu'on fait aujourd'hui

### Pendant la session
- Maximum 1 composant ou 1 feature par conversation
- Si une décision importante est prise → le noter immédiatement
- Si quelque chose semble incohérent avec le design system → stopper et signaler

### Fermeture
1. Mettre à jour Changelog.md
2. Mettre à jour Roadmap.md
3. Mettre à jour CLAUDE.md si nouveaux tokens/patterns découverts
4. Créer un fichier Decision-Log si décision importante prise

---

## 3. Gestion du design system

### Source de vérité
- Figma = source de vérité visuelle
- CLAUDE.md du projet = source de vérité technique
- Ces deux fichiers doivent toujours être alignés

### Quand lire Figma
- Avant chaque nouveau composant → lire le frame via Figma MCP
- En cas de doute sur un token ou une valeur → vérifier dans Figma
- Ne jamais supposer une valeur, toujours vérifier

### Pipeline token
Figma Variables → CLAUDE.md → tokens.css → composants
Aucun saut dans cette chaîne n'est autorisé.

---

## 4. Gestion de la codebase (pour non-codeur)

### Ce que Claude doit toujours faire
- Expliquer en 1 phrase ce que chaque composant fait
- Signaler si une modification risque de casser autre chose
- Ne jamais supprimer du code existant sans confirmation explicite
- Ne jamais ajouter de dépendance sans confirmation explicite

### Ce que Claude ne fait jamais sans confirmation
- Supprimer des fichiers
- Modifier la structure de dossiers
- Changer le nom d'un token ou composant existant
- Ajouter une librairie externe

### Audit mensuel
Une fois par mois, lancer : "Audite la codebase [PROJET] pour :
duplications, patterns incohérents, valeurs brutes, composants inutilisés"

---

## 5. Contrôle qualité

### Avant de livrer un composant
- [ ] Tous les tokens CSS utilisés (zéro valeur brute)
- [ ] Toutes les variantes du design system couvertes
- [ ] Props TypeScript typées
- [ ] États interactifs fonctionnels (hover, focus, disabled)
- [ ] Nommage cohérent avec Figma

### Signaux d'alerte à surveiller
- Claude génère du code avec des valeurs brutes → arrêter
- Un composant dépasse 100 lignes → découper
- La même valeur apparaît à plusieurs endroits → créer un token
- Claude ne sait pas d'où vient une valeur → vérifier dans Figma

---

## 6. Gestion des projets dans Obsidian

### Structure obligatoire par projet
```
01-Projects/[NOM]/
  CLAUDE.md          ← contexte technique, tokens, stack
  PRD.md             ← problème, objectif, périmètre
  Roadmap.md         ← todo / in-progress / done / blocked
  Changelog.md       ← entrées datées de chaque session
```

### Decision-Log
- Un fichier par décision importante
- Format : 04-Decision-Log/YYYY-MM-DD-[PROJET]-[sujet].md
- Frontmatter : type, project, date, status, context, decision, consequences
- Toute décision qui change la direction d'un projet doit être loguée

### Tokens de fenêtre
- Garder les conversations sous 60% de la fenêtre de tokens
- Une conversation = une tâche atomique
- Le CLAUDE.md charge le contexte, pas l'historique de chat
