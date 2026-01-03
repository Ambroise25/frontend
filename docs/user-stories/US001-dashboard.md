# US001 - Dashboard principal

## User Story

**En tant que** operateur  
**Je veux** voir un tableau de bord avec l'etat des traitements  
**Afin de** suivre les emails et demandes en temps reel

---

## Criteres d'acceptation

### Scenario 1: Affichage indicateurs
**Donne** des donnees dans le systeme  
**Quand** j'accede au dashboard  
**Alors** je vois:
- Nombre d'emails traites aujourd'hui
- Nombre en attente de validation
- Nombre d'erreurs
- Derniers emails recus

### Scenario 2: Navigation rapide
**Donne** le dashboard affiche  
**Quand** je clique sur un email  
**Alors** je suis redirige vers le detail pour validation

---

## Maquette

```
┌─────────────────────────────────────────────────────────────────┐
│  Email2Extranet Dashboard                                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐        │
│  │    12    │  │    3     │  │    1     │  │   156    │        │
│  │ Traites  │  │ En       │  │ Erreurs  │  │  Total   │        │
│  │ aujourd  │  │ attente  │  │          │  │ demandes │        │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘        │
│                                                                  │
│  Derniers emails                                     [Voir tout] │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ 14:30 │ Foncia    │ RECHERCHE FUITE... │ ✓ Traite │ [Voir] ││
│  │ 14:15 │ Nexity    │ REPARATION...      │ ⏳ Attente│ [Voir] ││
│  │ 13:45 │ Inconnu   │ Demande intervention│ ⚠ Erreur │ [Voir] ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  Graphique demandes (7 derniers jours)                          │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │     ▄   ▄▄                                                  ││
│  │  ▄▄ █ ▄ ██ ▄▄                                              ││
│  │  ██ █ █ ██ ██ ▄▄                                           ││
│  │  Lu Ma Me Je Ve Sa Di                                       ││
│  └─────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────┘
```

---

## Composants React

```
Dashboard/
├── StatsCards.tsx        # Les 4 cartes indicateurs
├── RecentEmails.tsx      # Liste des derniers emails
├── WeeklyChart.tsx       # Graphique 7 jours
└── index.tsx             # Page principale
```

---

## Appels API

- `GET /api/stats` - Indicateurs globaux
- `GET /api/stats/recent` - Derniers emails
- Polling toutes les 30 secondes pour mise a jour

---

## Definition of Done

- [ ] Page dashboard avec layout responsive
- [ ] 4 cartes statistiques
- [ ] Liste derniers emails avec statut
- [ ] Navigation vers detail
- [ ] Graphique 7 jours
- [ ] Rafraichissement automatique
- [ ] Tests composants
