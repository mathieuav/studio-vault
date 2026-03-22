# Studio Playbook — AI-Powered Solo Product Studio

> Source : recherche approfondie 400+ sources, Mars 2026
> Ce document est la référence permanente du studio.
> Il évolue uniquement quand on apprend quelque chose de nouveau.

---

## Philosophie

- **KISS** : une tâche = une conversation = un fichier de sortie
- **Lean** : construire le minimum, mesurer, itérer
- **Mémoire dans les fichiers** : Claude n'a pas de mémoire — les fichiers sont sa mémoire
- **Design Thinking** : toujours partir du problème utilisateur, pas de la solution
- Le non-codeur ne code pas — il est **architecte d'intention**

---

## Stack validée (Mars 2026)

| Outil | Rôle | Coût |
|-------|------|------|
| Obsidian-Studio | Cerveau / mémoire / PM | 4€/mois |
| Claude Desktop | AI core + Desktop Commander + Figma MCP | 20$/mois |
| Figma | Design + variables/tokens | existant |
| GitHub Free | Versioning + CI | 0€ |
| Vercel/Netlify Free | Déploiement | 0€ |
| Cursor Pro | Édition code avec contexte | 20$/mois |
| PostHog Free | Analytics (1M events) | 0€ |
| **Total** | | **~44-59€/mois** |

---

## Structure du vault Obsidian

```
00-Inbox/          → capture rapide, vider 1x/semaine
01-Projects/       → un dossier par projet actif
02-Areas/          → responsabilités continues sans deadline
03-Resources/      → savoir permanent (ce fichier est ici)
04-Decision-Log/   → une décision = un fichier, tagué par projet
_Templates/        → templates Templater
_Bases/            → dashboards Obsidian Bases
_Daily/            → notes quotidiennes
```

---

## Anatomie d'un projet

Chaque dossier dans `01-Projects/` contient :
- `CLAUDE.md` — contexte technique, tokens, stack, règles de génération
- `PRD.md` — problème, objectif, périmètre, critères de succès
- `Roadmap.md` — statuts : todo / in-progress / done / blocked
- `Changelog.md` — historique daté de tout ce qui a été fait

---

## Règles de session (TOUJOURS respecter)

1. `/start [PROJET]` en début de session
2. `/end [PROJET]` en fin de session
3. Une conversation = une tâche atomique
4. Fenêtre de tokens < 60% — conversations courtes
5. Ne jamais copier-coller du code dans le chat
6. Claude lit les fichiers directement depuis le vault

---

## Pipeline Figma → Code

1. Ouvrir le fichier Figma Desktop, sélectionner un frame
2. `/start [PROJET]` — charge le contexte
3. Donner le lien Figma du composant à Claude
4. Claude lit via Figma MCP → génère le code React/Tailwind
5. Coller dans Cursor / repo GitHub
6. `/end [PROJET]` — met à jour les fichiers

---

## Rendre le design system lisible par l'IA (méthode Pandya)

- **Spec files** : un fichier markdown par composant dans `specs/components/`
- **Token layer fermé** : `tokens.css` avec 3 niveaux (upstream → alias → component)
- **Zéro valeur brute** dans le code — toujours `var(--token-name)`
- **Nommage sémantique** : `color-action-primary-hover` pas `blue-500`
- **CLAUDE.md** contient toujours la liste complète des tokens du projet

---

## Contrôle de la codebase sans coder

- `CLAUDE.md` = règles permanentes que Claude lit avant chaque tâche
- `SYSTEM_ARCHITECTURE.md` = description plain-english des objets et relations
- Prompts courts et contraints : "garde les fonctions sous 30 lignes, utilise les composants existants"
- Refactoring mensuel : "audite ce code pour les doublons et les patterns incohérents"
- GitHub Desktop pour le versioning — pas de terminal nécessaire

---

## Méthode de validation lean (boucle rapide)

1. Design Figma → code via MCP
2. Deploy Vercel (preview URL instantanée)
3. Montrer à 5-10 utilisateurs cibles
4. Mesurer avec PostHog
5. Pivot ou itération selon les données

---

## Plugins Obsidian recommandés (Mars 2026)

| Plugin | Usage | Statut |
|--------|-------|--------|
| Bases | Dashboards sans code | ✅ Core plugin actif |
| Templater | Auto-templates par dossier | ✅ Stable, 4.4k stars |
| Obsidian Git | Backup auto GitHub | ✅ Stable |
| Excalidraw | Wireframes dans le vault | ✅ Très actif |
| Tasks | Gestion des tâches | ✅ Stable |
| Kanban | Board de tâches | ⚠️ Cherche maintainer |

---

## Ressources clés

- Figma MCP guide : https://github.com/figma/mcp-server-guide
- LLM Design Systems : https://hvpandya.com/llm-design-systems
- 63 Design Skills Claude : https://marieclairedean.substack.com
- Naming for AI : https://classnames.paulrobertlloyd.com
- Reduce token usage Figma : https://www.royvillasana.com/blog/figma-to-ai-prompter-reduce-token-usage
