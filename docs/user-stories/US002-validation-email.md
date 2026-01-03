# US002 - Validation et correction des donnees extraites

## User Story

**En tant que** operateur  
**Je veux** valider et corriger les donnees extraites d'un email  
**Afin de** m'assurer que les informations sont correctes avant envoi au CRM

---

## Criteres d'acceptation

### Scenario 1: Affichage donnees extraites
**Donne** un email parse  
**Quand** j'accede au detail  
**Alors** je vois:
- Email original (readonly)
- Donnees extraites (editable)
- Score de confiance par champ

### Scenario 2: Correction manuelle
**Donne** une adresse mal extraite  
**Quand** je modifie le champ adresse  
**Alors** le champ est mis a jour et marque "corrige"

### Scenario 3: Validation et envoi
**Donne** des donnees corrigees  
**Quand** je clique sur "Valider et envoyer"  
**Alors** les donnees sont envoyees a l'API CRM et l'email est marque "traite"

### Scenario 4: Selection bien existant
**Donne** une recherche retourne des biens similaires  
**Quand** je selectionne un bien existant  
**Alors** la demande sera rattachee a ce bien

---

## Maquette

```
┌─────────────────────────────────────────────────────────────────────────┐
│  Email #12345 - Foncia                                    [< Retour]    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  ┌─────────────────────────────┬────────────────────────────────────────┐│
│  │     EMAIL ORIGINAL          │      DONNEES EXTRAITES                 ││
│  │                             │                                        ││
│  │  De: no-reply@foncia.com    │  Bien                                  ││
│  │  Objet: Ordre de service... │  ┌────────────────────────────────────┐││
│  │                             │  │ Adresse *         [95%]            │││
│  │  Bonjour,                   │  │ 29 RUE DES ECONDEAUX               │││
│  │                             │  ├────────────────────────────────────┤││
│  │  En notre qualite de        │  │ Code postal *     [98%]            │││
│  │  syndic...                  │  │ 93800                              │││
│  │                             │  ├────────────────────────────────────┤││
│  │  Immeuble N° 501147727:     │  │ Ville *           [98%]            │││
│  │  LES AURELLES 4 - REF 6411  │  │ EPINAY SUR SEINE                   │││
│  │  29/31/33 RUE DES ECONDEAU  │  └────────────────────────────────────┘││
│  │  93800 EPINAY SUR SEINE     │                                        ││
│  │                             │  Bien existant trouve:                 ││
│  │  Objet: RECHERCHE DE FUITE  │  ○ 29/31/33 RUE DES ECONDEAUX (95%)   ││
│  │  MME PALENA / TOUZARD       │  ○ Creer nouveau bien                  ││
│  │                             │                                        ││
│  │  Contacts sur place:        │  Demande                               ││
│  │  - CHARLINE ET JULIE        │  ┌────────────────────────────────────┐││
│  │    +33651820580             │  │ Objet *           [92%]            │││
│  │                             │  │ RECHERCHE DE FUITE MME PALENA      │││
│  │  Cordialement,              │  ├────────────────────────────────────┤││
│  │  Marine ZOZAYA VIRION       │  │ Metier *                           │││
│  │  Foncia Vaucelles           │  │ [Etancheite        ▼]              │││
│  │                             │  ├────────────────────────────────────┤││
│  │                             │  │ Detail                             │││
│  │                             │  │ [Corps de l'email...]              │││
│  │                             │  ├────────────────────────────────────┤││
│  │                             │  │ Gestionnaire *                     │││
│  │                             │  │ [Marine ZOZAYA - Foncia ▼]         │││
│  │                             │  └────────────────────────────────────┘││
│  └─────────────────────────────┴────────────────────────────────────────┘│
│                                                                          │
│  ┌──────────────┐  ┌──────────────────┐  ┌──────────────────────────┐   │
│  │   Rejeter    │  │ Mettre en attente │  │  ✓ Valider et envoyer   │   │
│  └──────────────┘  └──────────────────┘  └──────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Composants React

```
EmailValidation/
├── EmailOriginal.tsx     # Affichage email readonly
├── ExtractedData.tsx     # Formulaire editable
├── ConfidenceIndicator.tsx # Badge score confiance
├── BienMatcher.tsx       # Selection bien existant
├── ActionButtons.tsx     # Valider, Rejeter, Attente
└── index.tsx             # Page principale
```

---

## Appels API

- `GET /api/emails/:id` - Recuperer email et donnees extraites
- `GET /api/biens/search` - Chercher biens similaires
- `POST /api/biens` - Creer nouveau bien
- `POST /api/demandes` - Creer demande
- `PUT /api/emails/:id/status` - Mettre a jour statut email

---

## Definition of Done

- [ ] Layout deux colonnes (email | formulaire)
- [ ] Affichage email original
- [ ] Formulaire editable avec tous les champs
- [ ] Indicateurs de confiance
- [ ] Recherche et selection bien existant
- [ ] Boutons d'action (Valider, Rejeter, Attente)
- [ ] Validation formulaire avant envoi
- [ ] Feedback succes/erreur
- [ ] Tests composants et integration
