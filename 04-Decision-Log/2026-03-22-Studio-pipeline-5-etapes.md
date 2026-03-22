---
type: decision
project: Studio-Workflow
date: 2026-03-22
status: decided
---

## Context
Le workflow qu'on construit n'est pas qu'un projet de design system.
Il faut une vision claire de ce qu'on veut atteindre à terme.

## Decision
Le pipeline complet se décompose en 5 étapes progressives :
1. Design system — tokens + composants React/Tailwind
2. AI design dans Figma avec les composants existants
3. Live prototype de nouvelles pages depuis le code
4. Build de nouvelles features produit en autonomie
5. Claude avec contexte produit complet comme partenaire de product design

## Consequences
- Chaque étape débloque la suivante — ne pas brûler les étapes
- Fountain-DS est le terrain de jeu pour valider tout le pipeline
- Le design system n'est pas la destination, c'est la fondation
