---
type: decision
project: Fountain-DS
date: 2026-03-22
status: decided
---

## Context
Comment maintenir la mémoire et le contexte Claude d'une session à l'autre
sans dépasser 60% de la fenêtre de tokens, sans copier-coller manuel.

## Decision
Utiliser des commandes Claude slash (/start, /end) qui lisent et écrivent
directement dans les fichiers Obsidian du projet via Desktop Commander.
La mémoire est dans les fichiers, pas dans le contexte de conversation.

## Consequences
- Chaque session commence avec /start [PROJET] → contexte chargé en 3 phrases
- Chaque session se ferme avec /end [PROJET] → Changelog, Roadmap, CLAUDE.md mis à jour automatiquement
- Conversations courtes et atomiques : une tâche = une conversation
- Zéro risque de dépassement de tokens sur des sessions longues
