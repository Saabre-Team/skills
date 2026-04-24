---
name: design-prototype
description: >
  Structure and improve a prototype, mockup, or wireframe request before building it with an AI tool
  (Figma Make, Claude artifacts, v0, Cursor, etc.). Use when someone wants to create a UI, screen,
  landing page, dashboard, or component and wants a better result than a generic AI output.
  Triggers on: "prototype", "maquette", "wireframe", "mockup", "crée-moi une interface",
  "génère un écran", "fais-moi une page", "design de", "UI pour", "landing page",
  "dashboard visuel", "composant UI", "crée une page web".
  Always use this skill when the user is about to prompt an AI tool to generate a visual interface
  — the goal is to get a precise, intentional result instead of AI slop.
argument-hint: "<description de ce que vous voulez créer>"
---

# Design Prototype

Aide à structurer un prototype, une maquette ou un wireframe avant de le générer avec un outil IA,
pour obtenir un rendu intentionnel plutôt qu'un output générique.

## Usage

```
/design-prototype $ARGUMENTS
```

## Règle fondamentale — Report all before filtering

**Identifie et signale tous les risques de slop et les zones de flou dans le brief avant de générer quoi que ce soit.**
Ne filtre pas par importance à ce stade. Un prompt vague produit toujours un résultat générique.

Ce qui ne compte PAS comme review :
- "Ça semble correct" sans avoir vérifié les intentions de design
- Générer directement sans cadrer le brief
- Supposer l'audience, le contexte, ou le style sans le confirmer

---

## Workflow

### 1. Comprendre l'intention

Demande à l'utilisateur ce qu'il veut créer. Accepte n'importe quelle forme :
- Un écran ou une page ("une landing page pour une app SaaS")
- Un composant ("un tableau de bord avec des KPIs")
- Une maquette ("le wireframe de notre onboarding")
- Une idée vague ("quelque chose pour présenter nos offres")

### 2. Cadrer le brief (questions prioritaires)

Pose les questions dans cet ordre. Ne les envoie pas toutes d'un coup — commence par les plus importantes et complète au fil de la conversation :

**Priorité 1 — L'essentiel :**
- **Outil cible** : où va être généré ce prototype ? (Figma Make, Claude artifact, v0, Cursor, autre)
- **Audience** : qui va voir ou utiliser cet écran ? (client final, investisseur, équipe interne)
- **Objectif** : qu'est-ce que cet écran doit déclencher ? (achat, inscription, compréhension, validation)
- **Contexte** : c'est pour une présentation, un test utilisateur, un vrai produit ?

**Priorité 2 — Le style :**
- **Références visuelles** : cite 1 à 3 produits ou sites dont tu aimes le style
- **Palette** : couleurs existantes ou contraintes (charte, couleurs à éviter)
- **Niveau de détail** : wireframe basse fidélité, maquette haute fidélité, ou entre les deux ?
- **Responsive** : desktop, mobile, ou les deux ?

**Priorité 3 — Le contenu :**
- **Textes** : vrais textes ou placeholders ? (si placeholders, précise le ton)
- **Images/icônes** : génériques ok, ou contraintes spécifiques ?
- **Données** : chiffres réels, exemples représentatifs, ou fictifs ?

### 3. Détecter les risques de slop

Avant de générer le prompt, identifie et signale explicitement les patterns AI slop courants pour ce type de design.

#### Patterns à éviter absolument

**Structure / Layout**
- Hero générique : grand titre centré + sous-titre gris + bouton bleu + image stock à droite
- Cards identiques en grille 3 colonnes sans hiérarchie visuelle
- Section "Features" avec 6 icônes identiques alignées
- Footer copié-collé avec 4 colonnes génériques
- "Témoignages" avec avatars ronds et étoiles jaunes sans personnalité

**Typographie**
- Titres en Inter ou Roboto sans intention typographique
- Hiérarchie plate (tout le texte à la même taille relative)
- Line-height par défaut sur les grands titres
- Corps de texte trop long ou mal contrasté

**Couleurs**
- Bleu #3B82F6 (Tailwind blue-500) comme couleur primaire par défaut
- Dégradés bleu → violet sans raison
- Fond blanc pur (#FFFFFF) sans nuance
- Trop de couleurs d'accent sans système cohérent

**Contenu**
- Copy générique : "Innovation", "Solutions", "Transformez votre business", "Rejoignez des milliers d'entreprises"
- Lorem ipsum dans une maquette "haute fidélité"
- Chiffres inventés sans contexte ("99.9% uptime", "10x faster")
- Icônes FontAwesome par défaut sans cohérence de style

**UX / Comportement**
- Aucun état vide, état d'erreur, ou état chargement
- Boutons CTA sans logique de hiérarchie (tout est "primary")
- Formulaires sans labels ni feedback de validation
- Navigation sans indication de page active

### 4. Construire le prompt

Génère un prompt structuré et précis pour l'outil cible, en intégrant :

**Structure du prompt :**
```
CONTEXTE : [qui utilise cet écran, dans quel produit, pour quoi faire]
ÉCRAN À CRÉER : [description précise de ce qui doit apparaître]
STYLE VISUEL : [références, palette, typographie, niveau de détail]
CONTENU : [vrais textes ou exemples représentatifs — jamais de lorem ipsum]
CONTRAINTES TECHNIQUES : [taille, responsive, framework si applicable]
À ÉVITER : [liste des patterns slop identifiés pour ce cas précis]
CRITÈRE DE RÉUSSITE : [comment sait-on que le résultat est bon]
```

**Règles de prompt :**
- Sois chirurgical sur le layout : décris la structure section par section
- Donne des exemples de textes réels, pas des placeholders
- Nomme les références visuelles précisément ("comme Linear.app", "dans le style de Vercel")
- Précise ce qu'on NE veut pas (les négatifs guident autant que les positifs)
- Si tu connais le framework cible (Tailwind, MUI, etc.), adapte la terminologie

### 5. Itérer sur le résultat

Après génération, propose systématiquement une checklist de review :

**Vérification anti-slop :**
- [ ] Le layout a une hiérarchie visuelle claire — un seul point focal principal
- [ ] La typographie est intentionnelle — tailles, poids, et espacements cohérents
- [ ] Les couleurs suivent un système — primaire, secondaire, neutrals définis
- [ ] Le contenu est représentatif — pas de lorem ipsum ni de chiffres inventés au hasard
- [ ] Les composants ont des états — hover, actif, désactivé, vide
- [ ] L'écran répond à son objectif — est-ce que l'action principale est évidente ?

**Questions de validation :**
- Est-ce qu'on distingue immédiatement l'action principale sur cet écran ?
- Est-ce que ce design pourrait passer pour du travail humain intentionnel ?
- Est-ce qu'il y a au moins une décision de design non-générique (couleur, typo, layout) ?

---

## Done when

- [ ] Le brief est cadré : outil, audience, objectif, style connus
- [ ] Les risques de slop spécifiques à ce design ont été identifiés et listés
- [ ] Le prompt est structuré avec les 7 composants (contexte, écran, style, contenu, contraintes, à éviter, critère)
- [ ] Le prompt contient de vrais textes ou exemples représentatifs — aucun lorem ipsum
- [ ] La checklist anti-slop est disponible pour review post-génération

---

## Référence — Patterns de qualité

### Ce qui distingue un bon design AI d'un AI slop

| Dimension | AI Slop | Design intentionnel |
|-----------|---------|---------------------|
| Layout | Grille symétrique par défaut | Hiérarchie visuelle avec point focal clair |
| Typographie | Inter 16px partout | Échelle typographique avec intention |
| Couleurs | Bleu Tailwind + gris | Palette définie avec tokens nommés |
| Contenu | Lorem ipsum / chiffres fictifs | Textes représentatifs du vrai usage |
| Composants | Boutons identiques, cards génériques | États définis, hiérarchie CTA claire |
| Personnalité | Pourrait être n'importe quel produit | Reconnaissable, mémorable, cohérent |

### Références de qualité à citer dans vos prompts

- **Apps SaaS B2B** : Linear, Vercel, Resend, Raycast
- **Marketing / Landing** : Stripe, Clerk, Loom
- **Dashboards** : Retool, Metabase (version dark), Grafana (version moderne)
- **Onboarding / Mobile** : Duolingo, Notion, Arc Browser
- **Design system visible** : Radix, shadcn/ui, Primer (GitHub)
