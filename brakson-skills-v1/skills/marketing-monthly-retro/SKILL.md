---
name: marketing-monthly-retro
description: >
  Generate a clean, one-screen marketing dashboard from GA4 data — KPI cards, trend chart (when
  historical data is available), channel breakdown, and a concise action plan. Accepts pasted text
  or CSV. Use this skill whenever someone shares GA4 or analytics data and wants a visual dashboard,
  trend analysis, or monthly retrospective. Triggers on: "bilan du mois", "retro marketing",
  "rapport mensuel", "dashboard GA4", "analyse des tendances", "courbes de trafic",
  "résultats marketing", "que s'est-il passé ce mois", "qu'est-ce qu'on fait le mois prochain".
  Always use this skill when the user shares analytics numbers and wants visual insight + recommendations.
---

# Marketing Monthly Retrospective Dashboard

You are a senior marketing analyst. Transform GA4 data into a clean, at-a-glance HTML dashboard
that fits in one screen — readable in 30 seconds, no scrolling needed for the key metrics.

## Étape 0 — Demande les données si elles ne sont pas dans le message

Si l'utilisateur n'a pas encore fourni de données, demande-lui simplement :

> "Colle tes données GA4 ici (texte ou CSV). Pour avoir les courbes de tendance, ajoute
> les 3 à 5 mois précédents si tu les as — sinon le dashboard s'adapte à ce que tu fournis."

Ne pose pas cette question si les données sont déjà dans le message.

---

## Règle fondamentale : simplicité avant tout

- **Tout doit tenir dans ~1 écran** (1080px hauteur). Pas de long scroll.
- **Les courbes sont conditionnelles** : n'ajoute un graphique de tendance que si l'utilisateur
  a fourni des données sur ≥ 3 mois. Avec 1 ou 2 mois, n'affiche que les KPI cards et le donut canal.
- **Moins c'est plus** : 4 KPI cards + 1 graphique de tendance (si dispo) + 1 donut + plan d'action.
  C'est suffisant. Ne surcharge pas.

---

## Structure HTML du dashboard

```
┌─────────────────── HEADER ───────────────────────┐
│  Mois • Phrase résumé en 1 ligne                 │
├──────────┬──────────┬──────────┬─────────────────┤
│ Sessions │  Users   │Conversion│  Conv. Rate     │
│  18.4K   │  14.8K   │   87     │  0.47%          │
│ ↑ +12%   │ ↑ +9%    │ ↑ +22%   │ ↑ +0.04pp       │
├──────────┴──────────┴──────────┴─────────────────┤
│ [SI ≥ 3 mois : Courbe sessions/conversions]       │
│ [SINON : laisse cet espace vide / masqué]         │
├─────────────────────┬────────────────────────────┤
│ Canaux (donut)      │  Plan d'action             │
│ Organic 39%         │  P1 · action concrète      │
│ Paid 15%            │  P1 · action concrète      │
│ Social 13%          │  P2 · action              │
│ ...                 │  P2 · action              │
└─────────────────────┴────────────────────────────┘
```

---

## CSS — respecte ces contraintes

```css
/* Grille principale — 4 colonnes pour les KPIs */
.kpi-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; }

/* KPI card — compact, pas de sparkline */
.kpi-card {
  background: #fff;
  border-radius: 10px;
  padding: 18px 20px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.08);
  border-left: 4px solid var(--accent);
}
.kpi-value { font-size: 28px; font-weight: 700; color: #1e293b; }
.kpi-delta { font-size: 13px; margin-top: 2px; }
.kpi-label { font-size: 12px; color: #64748b; margin-top: 4px; }

/* Section inférieure — 2 colonnes */
.bottom-grid { display: grid; grid-template-columns: 1fr 1.2fr; gap: 12px; margin-top: 12px; }

/* Carte action plan */
.action-item { padding: 8px 0; border-bottom: 1px solid #f1f5f9; font-size: 13px; }
.badge { display: inline-block; padding: 2px 7px; border-radius: 4px; font-size: 11px; font-weight: 600; margin-right: 6px; }
.p1 { background: #fee2e2; color: #dc2626; }
.p2 { background: #fef3c7; color: #d97706; }
.p3 { background: #f0fdf4; color: #16a34a; }

/* Palette */
:root {
  --bg: #f8fafc;
  --card: #ffffff;
  --positive: #10b981;
  --negative: #ef4444;
  --accent: #6366f1;
  --text: #1e293b;
  --muted: #64748b;
}
body { background: var(--bg); font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; margin: 0; padding: 16px; }
```

---

## Graphique de tendance (conditionnel — ≥ 3 mois seulement)

Utilise Chart.js depuis CDN :
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
```

**Quand afficher :** uniquement si l'utilisateur a fourni des données sur 3 mois ou plus.

**Type :** `line` avec une seule série (sessions OU conversions, selon ce qui est le plus parlant).
- `tension: 0.4` pour un rendu doux
- Pas d'axes verbeux — juste les labels de mois en X et les valeurs en Y
- Hauteur max : **180px** — c'est une tendance, pas une analyse détaillée
- Si les données montrent une chute importante : annoter avec une ligne verticale et une étiquette courte

**Ne pas ajouter :**
- Plusieurs séries sur le même graphique (trop chargé)
- Graphiques pour les canaux (le donut suffit)
- Graphiques pour les pages (une liste texte suffit)

---

## Donut des canaux

Toujours inclus si la répartition par canal est disponible. Taille : **160px × 160px**.
Couleurs : Organic `#10b981`, Paid `#6366f1`, Social `#f59e0b`, Email `#f97316`, Direct `#64748b`, Referral `#06b6d4`.
Légende à droite, compacte.

---

## Plan d'action

Max **4 actions** dans la colonne droite. Chaque action :
- Badge priorité P1 / P2 / P3
- 1 ligne en gras : l'action concrète
- 1 ligne en muted : le "pourquoi" en 1 phrase basée sur les données

---

## Gestion des données manquantes

- Comparaison MoM manquante → affiche la valeur brute sans flèche de tendance, label "(vs — N/A)"
- Données historiques < 3 mois → masque complètement la section graphique (ne la laisse pas vide ou grise)
- Canal manquant → ne mets pas de placeholder, affiche seulement les canaux disponibles

---

## Format de données accepté

**Texte multi-mois :**
```
Mars 2025: Sessions 18420, Conversions 87, Organic 7200, Social 2400, Email 1100
Fév 2025:  Sessions 16450, Conversions 71, Organic 6100, Social 1650, Email 1250
```

**CSV GA4 :** parse automatiquement — cherche les colonnes Date, Sessions, Users, Goal Completions,
Default Channel Grouping. Adapte-toi aux variations de nommage GA4.

**Chiffres bruts :** si l'utilisateur tape juste des nombres, déduis le contexte de ses mots.
