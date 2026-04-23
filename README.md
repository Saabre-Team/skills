# Brakson Skills Library

Bibliothèque de skills Claude conçue pour les équipes Brakson. Un **skill** est une instruction structurée qui transforme Claude en expert métier sur une tâche précise — analyse data, rédaction commerciale, planning produit, support client.

## Qu'est-ce qu'un skill ?

Un skill, c'est un raccourci intelligent. Au lieu de reformuler à chaque fois votre besoin à Claude, vous tapez `/nom-du-skill` et Claude adopte immédiatement le bon rôle, le bon format de sortie, et les bonnes règles de vérification pour la tâche.

**Exemple concret :**
- Sans skill → *"Analyse ces données GA4 et fais-moi un dashboard marketing avec les KPIs, les tendances, et des recommandations pour le mois prochain"*
- Avec skill → `/marketing-monthly-retro` puis coller les données

Le skill garantit un rendu cohérent, structuré et vérifiable à chaque utilisation.

## Installation

1. Télécharger `brakson-skills-v1.plugin`
2. Dans Claude → Paramètres → Plugins → Importer
3. Les 31 skills sont disponibles via `/nom-du-skill`

## Les 31 skills

### Marketing (7)
| Skill | Usage |
|-------|-------|
| `marketing-monthly-retro` ⭐ | Dashboard GA4 mensuel — coller un export et obtenir KPIs + plan d'action |
| `campaign-plan` | Structurer un plan de campagne avec actions et dépendances |
| `email-sequence` | Rédiger une séquence email avec objectif et persona |
| `content-creation` | Produire du contenu adapté au canal et à l'audience |
| `seo-audit` | Auditer une page ou un site avec recommandations priorisées |
| `brand-review` | Évaluer la cohérence de marque sur un asset ou une copie |
| `performance-report` | Synthétiser les résultats d'une période avec vérification des chiffres |

### Product Owner (8)
| Skill | Usage |
|-------|-------|
| `write-spec` | Rédiger une spec avec tâches atomiques et critères "Done when" |
| `sprint-planning` | Structurer un sprint avec tâches vérifiables et critères d'acceptation |
| `roadmap-update` | Mettre à jour une roadmap avec milestones atomiques |
| `stakeholder-update` | Préparer une communication claire pour les parties prenantes |
| `synthesize-research` | Consolider des notes de recherche en insights actionnables |
| `metrics-review` | Passer en revue les métriques avec cross-check obligatoire |
| `product-brainstorming` | Générer et structurer des idées produit |
| `ux-copy` | Rédiger ou revoir des textes d'interface utilisateur |

### Data (4)
| Skill | Usage |
|-------|-------|
| `analyze` | Analyser des données — du lookup simple à l'analyse complète |
| `sql-queries` | Écrire et vérifier des requêtes SQL |
| `build-dashboard` | Construire un dashboard avec checklist de vérification |
| `validate-data` | Valider un jeu de données avant signature — aucun "looks good" sans vérification |

### Customer Support (5)
| Skill | Usage |
|-------|-------|
| `ticket-triage` | Classer et prioriser des tickets entrants |
| `draft-response` | Rédiger une réponse client adaptée au contexte |
| `customer-research` | Synthétiser les retours clients en insights |
| `kb-article` | Rédiger un article de base de connaissance clair |
| `customer-escalation` | Gérer une escalade client avec le bon niveau de communication |

### Sales (7)
| Skill | Usage |
|-------|-------|
| `account-research` | Préparer un dossier compte avant un premier contact |
| `call-prep` | Préparer un appel commercial avec contexte et agenda |
| `call-summary` | Résumer un appel avec actions et prochaines étapes |
| `competitive-intelligence` | Analyser un concurrent sur des axes précis |
| `draft-outreach` | Rédiger un message de prospection personnalisé |
| `pipeline-review` | Passer en revue le pipeline avec actions par étape |
| `forecast` | Construire ou vérifier une prévision de vente |

## Règles d'hygiène appliquées

Les skills suivants intègrent des règles comportementales anti-slop pour garantir des sorties fiables :

- **write-spec / sprint-planning** — tâches atomiques + critère "Done when" obligatoire sur chaque item
- **validate-data / sql-queries** — vérification systématique avant toute validation, pas de "looks good" sans preuve
- **analyze / build-dashboard / metrics-review / performance-report** — cross-check des chiffres avant présentation
- **brand-review / campaign-plan / synthesize-research / roadmap-update** — tous les findings remontés avant filtrage

## Structure du repo

```
/
├── brakson-skills-v1.plugin   # Plugin installable (contient tous les skills)
├── README.md                  # Ce fichier
├── account-research.md        # Source des skills (format texte)
├── analyze.md
├── ...                        # 31 fichiers .md au total
```

Les fichiers `.md` sont les sources lisibles de chaque skill. Le `.plugin` est le package installable pour Claude.
