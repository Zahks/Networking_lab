## Structure Active Directory

Afin d'organiser les objets Active Directory et de faciliter l'administration, plusieurs unités d'organisation personnalisées ont été créées.

Cette structuration permet de séparer les utilisateurs, les ordinateurs et les groupes de sécurité afin de faciliter l'administration quotidienne et l'application des stratégies de groupe.

### Organisation générale

```text
lab.local
│
├── Domain Controllers
│   └── DC01
│
├── Utilisateurs
│   │
│   ├── IT
│   ├── RH
│   ├── Finance
│   └── Direction
│
├── Ordinateurs
│   └── DESKTOP-RNDT6FD
│
└── Groupe
```

---

### OU Utilisateurs

L'ensemble des utilisateurs métier est regroupé dans une unité d'organisation parent dédiée.

```text
Utilisateurs
│
├── IT
│   └── J. Awountsac
│
├── RH
│   └── A. Awountsac
│
├── Finance
│   └── M. Awountsac
│
└── Direction
    └── U. Awountsac
```

Chaque sous-OU représente un service de l'entreprise.

Cette organisation permet :

- une meilleure lisibilité de l'annuaire ;
- une administration simplifiée ;
- l'application ciblée des GPO ;
- une meilleure évolutivité de l'infrastructure.

---

### OU Ordinateurs

Les postes de travail du domaine sont regroupés dans une unité d'organisation dédiée.

```text
Ordinateurs
│
└── DESKTOP-RNDT6FD
```

Cette séparation permet d'appliquer des stratégies spécifiques aux postes du domaine indépendamment des utilisateurs.


## Groupes de sécurité

Afin de simplifier l'administration des permissions et de respecter les bonnes pratiques Active Directory, plusieurs groupes de sécurité ont été créés.

### Groupes métiers

```text
G_IT
G_RH
G_Finance
G_Direction
```

Ces groupes permettent de regrouper les utilisateurs selon leur service.

Exemple :

```text
J. Awountsac
        ↓
      G_IT
```

---

### Groupes d'accès

```text
G_Acces_IT
G_Acces_RH
G_Acces_Finance
G_Acces_Direction
```

Ces groupes servent à attribuer les permissions sur les ressources partagées.

Cette approche permet d'administrer les accès via des groupes plutôt que directement sur les comptes utilisateurs.

---

### Exemple d'organisation des droits

```text
M. Awountsac
        ↓
     G_Finance
        ↓
 G_Acces_Finance
        ↓
 Dossier Finance
```

---

### Avantages

- administration simplifiée ;
- gestion centralisée des accès ;
- évolutivité ;
- application des bonnes pratiques Active Directory ;
- réduction du risque d'erreurs lors de l'attribution des permissions.

## Authentification

Une fois intégré au domaine, un utilisateur peut ouvrir une session à l'aide de son compte Active Directory.

Exemple :

```text
LAB\mawountsac
```

ou

```text
LAB\jawountsac
``

L'authentification est réalisée par le contrôleur de domaine DC01 qui vérifie l'identité de l'utilisateur dans Active Directory.


