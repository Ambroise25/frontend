# US003 - Liste des biens et demandes

## User Story

**En tant que** operateur  
**Je veux** consulter la liste des biens et leurs demandes  
**Afin de** avoir une vue d'ensemble et retrouver des informations

---

## Criteres d'acceptation

### Scenario 1: Liste des biens
**Donne** des biens en base  
**Quand** j'accede a la page Biens  
**Alors** je vois la liste paginee avec recherche

### Scenario 2: Detail d'un bien
**Donne** un bien avec 5 demandes  
**Quand** je clique sur le bien  
**Alors** je vois le detail et l'historique des demandes

### Scenario 3: Filtrer les demandes
**Donne** des demandes dans differents etats  
**Quand** je filtre par "en_cours"  
**Alors** seules les demandes en cours sont affichees

---

## Pages

### /biens - Liste des biens

```
┌─────────────────────────────────────────────────────────────────┐
│  Biens                                        [+ Nouveau bien]  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Recherche: [________________________] [Rechercher]             │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ Adresse                      │ Ville          │ Demandes    ││
│  ├─────────────────────────────────────────────────────────────┤│
│  │ 29/31/33 RUE DES ECONDEAUX  │ EPINAY S/SEINE │ 5           ││
│  │ 12 RUE DE PARIS             │ TAVERNY        │ 3           ││
│  │ 45 AVENUE VICTOR HUGO       │ PARIS 16       │ 12          ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  [< Precedent]  Page 1 sur 8  [Suivant >]                       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### /biens/:id - Detail bien

```
┌─────────────────────────────────────────────────────────────────┐
│  29/31/33 RUE DES ECONDEAUX                     [< Retour]      │
│  93800 EPINAY SUR SEINE                                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Informations                                                    │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ Gestionnaire: Marine ZOZAYA (Foncia)                        ││
│  │ Reference: LES AURELLES 4 - REF 6411                        ││
│  │ Cree le: 14/10/2025                                         ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
│  Demandes (5)                               [+ Nouvelle demande] │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ # │ Date       │ Objet                    │ Etat           ││
│  ├─────────────────────────────────────────────────────────────┤│
│  │ 1 │ 14/10/2025 │ RECHERCHE FUITE PALENA   │ ✓ Terminee     ││
│  │ 2 │ 20/10/2025 │ REPARATION TERRASSE      │ ⏳ En cours    ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### /demandes - Liste des demandes

```
┌─────────────────────────────────────────────────────────────────┐
│  Demandes                                                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Filtres:                                                        │
│  Etat: [Tous ▼]  Metier: [Tous ▼]  Du: [____] Au: [____]       │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ # │ Date       │ Bien              │ Objet          │ Etat  ││
│  ├─────────────────────────────────────────────────────────────┤│
│  │ 1 │ 03/01/2026 │ 29 RUE ECONDEAUX  │ RECHERCHE...   │ Nouv  ││
│  │ 2 │ 02/01/2026 │ 12 RUE DE PARIS   │ REPARATION...  │ Cours ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Composants React

```
Biens/
├── BiensList.tsx         # Liste paginee
├── BienCard.tsx          # Carte resume
├── BienDetail.tsx        # Page detail
├── SearchBar.tsx         # Recherche
└── index.tsx

Demandes/
├── DemandesList.tsx      # Liste avec filtres
├── DemandeRow.tsx        # Ligne tableau
├── DemandeFilters.tsx    # Filtres etat/metier/date
├── DemandeDetail.tsx     # Detail complet
└── index.tsx
```

---

## Definition of Done

- [ ] Page liste biens avec pagination
- [ ] Recherche biens par adresse/ville
- [ ] Page detail bien avec demandes
- [ ] Page liste demandes avec filtres
- [ ] Detail demande
- [ ] Navigation entre pages
- [ ] Tests composants
