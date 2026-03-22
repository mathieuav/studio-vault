# CLAUDE.md — FountainX Design System

## Contexte projet
Tu travailles sur le design system FountainX pour le client Fountain.
L'objectif est de générer du code React + Tailwind CSS fidèle au design system Figma.
Ce fichier est ta source de vérité. Lis-le avant chaque tâche.

## Stack technique
- Framework : React (TypeScript)
- Styling : Tailwind CSS (classes utilitaires uniquement)
- Typo : CircularXX (Regular 400, Medium 500, Bold 700)
- Ne jamais installer Tailwind si non demandé
- Ne jamais utiliser de valeurs brutes — toujours les tokens CSS

---

## Design Tokens

### Couleurs — Neutral
```
--neutral/white : #ffffff
--neutral/50    : #f8fafc
--neutral/100   : #f1f5f9
--neutral/300   : #b7c0cb
--neutral/400   : #687281
--neutral/600   : #404d5f
--neutral/900   : #0f172a
```

### Couleurs — Brand
```
--brand/600 : #4f46e5
--brand/800 : #3730a3
```

### Couleurs — Semantic
```
--green/50  : #d8f9d3
--green/600 : #3e8334
--green/800 : #145b2f
--rose/600  : #e11d48
```

### Primary Button — Gradient
```
background: linear-gradient(to bottom, #3935ff, #8f00ff)
hover      : --brand/800 (#3730a3)
focus ring : --brand/600 (#4f46e5), 2px border, offset 2px
disabled   : --neutral/50 bg, --neutral/300 text
loading    : --brand/600 bg, opacity 60%, spinner icon
```

### Spacing
```
--spacing/0   : 0px
--spacing/0.5 : 2px
--spacing/1   : 4px
--spacing/2   : 8px
--spacing/3   : 12px
--spacing/4   : 16px
```

### Border Radius
```
--radius/radius-default : 4px
--radius/radius-lg      : 8px
--radius/radius-full    : 999px
```

---

## Composants existants

### Button
Props : variant (primary | secondary | text | success | danger)
        size (default | small)
        state (enabled | hover | focus | disabled | loading)
        startIcon (boolean)
        endIcon (boolean)

Règles :
- Un seul primary button par container
- Texte court (1-3 mots), sentence case ("Save changes")
- Éviter les disabled buttons si possible
- default : px-16px py-10px, radius-lg, text-14px Medium
- small   : px-12px py-6px,  radius-lg, text-14px Medium

---

## Typographie
```
CircularXX Medium  500 — 36px / lh 40px  → h1
CircularXX Medium  500 — 24px / lh 32px  → h3
CircularXX Medium  500 — 14px / lh 20px  → body2 / button label
CircularXX Regular 400 — 14px / lh 20px  → body1 / subtitle
CircularXX Regular 400 — 12px / lh 16px  → small
```

---

## Règles de génération de code

1. Toujours utiliser les tokens CSS (ex: `text-[color:var(--neutral/900)]`)
2. Ne jamais coder de valeur brute (#0f172a) directement — utiliser le token
3. Respecter les data-name des layers Figma comme noms de composants
4. Générer des composants TypeScript avec props typées
5. Suivre exactement les variantes et états documentés ci-dessus
6. Lien Figma source : https://www.figma.com/design/8SOWLEPyd724hQBE8cfFvI/FountainX-Design-System
