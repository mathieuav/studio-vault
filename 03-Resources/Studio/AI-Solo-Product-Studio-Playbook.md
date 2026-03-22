# AI-Powered Solo Product Studio — Playbook
*Généré le 2026-03-22 — Recherche sur 400+ sources*

## TL;DR
Un designer senior peut gérer un cycle produit complet (recherche → design → code → déploiement)
pour moins de 75€/mois. Le secret : être architecte d'intention, pas codeur.
La mémoire est dans les fichiers. Une conversation = une tâche atomique.

---

## 1. Obsidian comme cerveau du studio

### Stack plugins recommandée (Mars 2026)
- **Bases** (core plugin) — dashboards no-code, remplace Dataview pour 90% des usages
- **Dataview** — requêtes complexes, en maintenance mais fonctionnel
- **Templater** — automation à la création de notes, très actif (v2.18.1)
- **Excalidraw** — whiteboard intégré, fichiers linkables dans le vault
- **Obsidian Git** — backup auto sur GitHub
- **Tasks** — gestion de tâches
- **QuickAdd** — capture rapide

### Plugins à éviter
- **Projects plugin** — abandonné Mai 2025
- **Kanban** — "looking for new maintainers", bugs non résolus

### Structure vault recommandée
```
00-Inbox/          capture rapide, triage hebdo
01-Projects/       un dossier par projet actif
02-Areas/          responsabilités sans deadline
03-Resources/      savoir de référence
04-Decision-Log/   un fichier par décision, taggé par projet
_Templates/        templates Templater
_Bases/            dashboards
_Daily/            notes quotidiennes
```

### Frontmatter essentiel
Chaque note projet doit avoir : type, project, status, priority, quarter
Chaque décision doit avoir : type, project, date, status, context, decision, consequences

---

## 2. Figma MCP Server — État Mars 2026

### Ce qui fonctionne
- `get_design_context` : extrait structure, tokens, props, screenshot d'un node
- `get_variable_defs` : récupère les variables Figma directement
- Réduction de 50-70% du temps sur les composants atomiques (boutons, inputs)
- Fonctionne avec Claude Desktop, Cursor, Windsurf

### Limitations connues
- Ne peut pas mettre à jour du code existant (génération uniquement)
- Erreur `response exceeds maximum allowed tokens` sur les gros fichiers
- Rate limits agressifs sur Starter (6 appels/mois !)
- Pas de boucle de raffinement visuel

### Bonne pratique
- Toujours sélectionner un layer dans Figma Desktop avant d'appeler le MCP
- Nommer les layers sémantiquement (CardContainer pas Group 5)
- Utiliser Auto Layout pour communiquer le comportement responsive
- Spécifier toujours le framework cible dans le prompt

---

## 3. Design System lisible par les LLMs

### Le problème
Les LLMs prennent 200-300 micro-décisions visuelles par session.
Sans contraintes, ils dérivent — session 10 ressemble à 3 produits différents.

### La méthode Pandyk (la plus complète)
4 couches :
1. **Spec files** — markdown structuré par composant, lu en début de session
2. **Closed token layer** — tokens CSS en 3 niveaux d'indirection, ensemble fermé
3. **Audit script** — détecte les valeurs brutes dans le code généré
4. **Drift detection** — pin les versions, alerte sur les changements upstream

### Naming convention tokens
Pattern : `{namespace}-{category}-{role}-{modifier}-{state}`
Exemple : `color-action-primary-hover`
3 tiers : global (blue-60) → semantic (color-brand-primary) → component (button-accent-bg-hover)

### Résultat documenté sur Atlaskit
Valeurs CSS hardcodées : 418 → 0
Tokens mappés : 230+

---

## 4. Pipeline Figma Tokens → Claude → Code

### Workflow recommandé
1. Figma Variables → Tokens Studio plugin (export JSON)
2. JSON → GitHub (commit via GitHub Desktop)
3. GitHub Actions → Style Dictionary → CSS/Tailwind output
4. CLAUDE.md référence le fichier tokens.css

### 4 méthodes pour injecter les tokens dans Claude
1. `tokens.css` à la racine + instruction CLAUDE.md
2. Figma MCP `get_variable_defs`
3. Spec files (méthode Pandya)
4. Claude Skill dédié au design system

### Export natif DTCG
Figma annoncé à Schema 2025, en cours de déploiement début 2026
Éliminera le besoin de Tokens Studio pour l'export

---

## 5. Claude Skills pour designers

### Différence Skills vs Projects
- Projects : "voici ce que tu dois savoir"
- Skills : "voici comment faire les choses" (auto-trigger, progressive disclosure)

### Collection MC Dean — 63 skills gratuits
GitHub : Owl-Listener/designer-skills (MIT)
8 plugins : research, systems, strategy, UI, interaction, prototyping, design ops, toolkit
Commandes clés : /discover, /strategize, /handoff, /ui-design:color-palette

### Skill officiel Anthropic Frontend Design
277,000+ installs — combat la "convergence distributionnelle" (designs génériques)

### Créer ses propres commandes
Fichiers .md dans ~/.claude/commands/
Nom du fichier = nom de la commande
$ARGUMENTS = paramètre passé après la commande

---

## 6. Connexion Obsidian ↔ Claude

### Méthode recommandée (la plus simple)
Anthropic filesystem MCP server → pointe sur le vault
Setup : éditer claude_desktop_config.json, 1 fichier JSON, Node.js requis

### Alternatives
- Obsidian REST API + mcp-obsidian (plus riche mais plus complexe)
- Desktop Commander (accès direct fichiers, pas de config MCP requise)
- Smart Connections (semantic search, local embeddings, offline)

---

## 7. Garder le contrôle d'une codebase qu'on ne comprend pas

### Documents obligatoires dans chaque projet
- **CLAUDE.md** — règles de code, tokens, conventions (lu automatiquement)
- **SYSTEM_ARCHITECTURE.md** — description plain-english des objets et relations
- **PROMPTING_PLAYBOOK.md** — exemples de bons/mauvais prompts pour ce projet

### Anti-code-rot
1. YAGNI extrême — supprimer agressivement les features inutiles
2. Naming greppable — chaque concept = un nom distinct
3. Pattern templates — 2-3 composants "golden" que Claude doit imiter
4. Prompts petits et contraints — "max 30 lignes par fonction"
5. Audit mensuel — "trouve les duplications et patterns incohérents"

### Progression tool recommandée
Débutant : v0.dev (prototypage) + GitHub Desktop (versioning)
Intermédiaire : Cursor Pro $20/mo (Visual Editor, codebase-aware)
Avancé : Claude Code (commandes custom, pipeline Figma MCP direct)

---

## 8. Design Thinking adapté à l'ère AI

### Ce qui a changé
Le prototype ne coûte plus rien → la logique "front-load la recherche" est obsolète
"En 2005, faire les choses était cher. Cette logique est cassée." — Jeff Humble

### Loop de validation lean AI
1. Design dans Figma (composants design system)
2. Figma MCP + Claude Code → code fonctionnel
3. Vercel free tier → déploiement en 2 minutes
4. 10 utilisateurs cibles — 8/10 voient la valeur = validé
5. PostHog (free) → mesure le comportement réel
6. Itérer dans Figma ou directement dans le code

### Thin slices > broad MVPs
Construire une expérience cohérente et complète pour UN cas d'usage précis
plutôt qu'une large surface peu profonde.

---

## 9. Stack complète et coûts

| Outil | Coût | Rôle |
|-------|------|------|
| Obsidian Sync | 4€/mo | Vault pro |
| Claude Pro | 20€/mo | AI core |
| Figma | 0-15€/mo | Design |
| Cursor Pro | 20€/mo | Code editing |
| GitHub Free | 0€ | Versioning |
| Vercel/Netlify | 0€ | Déploiement |
| PostHog Free | 0€ | Analytics |
| **Total** | **44-59€/mo** | |

### Notes importantes
- Vercel Hobby = usage non-commercial uniquement → Netlify pour les projets clients
- Railway a supprimé son free tier (Août 2023) → ne pas utiliser
- v0.dev free = bon pour prototyper, credit system brûle vite sur Pro
- Cursor pricing volatile → Windsurf 15€/mo comme backup

---

## 10. Ce qui fonctionne vs ce qui casse

### Intégrations naturelles ✅
- Obsidian → Claude via filesystem MCP : seamless
- Figma → Claude → Code via MCP : centre du workflow
- Design tokens → cohérence code : fonctionne si infrastructure faite en amont
- Claude Skills → workflows répétables : ROI très élevé

### Points de friction ⚠️
- Figma MCP → mise à jour code existant : ne fonctionne pas, workaround nécessaire
- Obsidian Kanban → fragile, utiliser Bases table en attendant la board view
- Token sync automation → nécessite GitHub Actions, pas zero-code
- Figma MCP rate limits sur Starter : inutilisable (6 appels/mois)

### Risques à surveiller 🔴
- Accumulation de code AI sans compréhension → dette technique
- Context window overflow → sessions atomiques obligatoires
- Cursor pricing volatility → avoir un backup prêt
- Kanban plugin abandon → migrer vers Bases dès que board view disponible
