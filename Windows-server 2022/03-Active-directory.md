# Active Directory

## Présentation

Active Directory est le service d'annuaire utilisé dans les environnements Microsoft pour centraliser l'authentification, l'administration des utilisateurs, des ordinateurs et l'application des stratégies de sécurité.

Dans ce laboratoire, Active Directory constitue le cœur de l'infrastructure. Il permet de gérer les comptes utilisateurs, les postes de travail et les stratégies de groupe à partir d'un point d'administration unique.

---

## Contrôleur de domaine

Le rôle Active Directory Domain Services (AD DS) a été installé sur le serveur :

```text
DC01
```

Adresse IP :

```text
192.168.1.10
```

Le serveur assure également le rôle DNS nécessaire au fonctionnement du domaine.

---

## Domaine Active Directory

### Forêt

```text
lab.local
```

### Domaine

```text
lab.local
```

### Nom NetBIOS

```text
LAB
```

Dans ce laboratoire, la forêt et le domaine sont identiques car l'infrastructure ne comporte qu'un seul domaine.

---

## Notions importantes

### Forêt (Forest)

La forêt représente le niveau logique le plus élevé d'Active Directory.

Elle constitue la frontière de confiance globale regroupant un ou plusieurs domaines.

Dans ce projet :

```text
Forêt = lab.local
```

---

### Domaine (Domain)

Le domaine représente une frontière administrative et de sécurité.

Il permet de centraliser :

- l'authentification ;
- les comptes utilisateurs ;
- les ordinateurs ;
- les stratégies de sécurité.

Dans ce projet :

```text
Domaine = lab.local
```

---

### Unité d'organisation (OU)

Les unités d'organisation permettent de structurer les objets Active Directory.

Elles facilitent :

- l'administration ;
- la délégation ;
- l'application des GPO.

---

## Structure Active Directory

Afin d'organiser les objets Active Directory et de faciliter l'administration, des unités d'organisation personnalisées ont été créées.

### OU Utilisateurs

L'ensemble des utilisateurs métier est regroupé dans une unité d'organisation parent dédiée.

```text
Utilisateurs
│
├── IT (J. Awountsac)
├── RH (A. Awountsac)
├── Finance (M. Awountsac)
└── Direction (U. Awountsac)
```

Chaque sous-OU représente un service de l'entreprise.

### Avantages:

- une meilleure lisibilité de l'annuaire ;
- une gestion simplifiée des utilisateurs ;
- l'application ciblée des GPO ;
- une meilleure évolutivité de l'infrastructure.

### OU Ordinateurs

Les postes de travail du domaine sont regroupés dans une OU spécifique :

```text
Ordinateurs
│
└── DESKTOP-RNDT6FD
```
## Groupes de sécurité

Afin de simplifier la gestion des permissions et de faciliter l'administration des ressources, plusieurs groupes de sécurité ont été créés.

### Groupes métiers

```text
G_IT
G_RH
G_FINANCE
G_DIRECTION
```

Ces groupes permettent de regrouper les utilisateurs en fonction de leur service.

### Groupes d'accès

```text
G_Acces_IT
G_Acces_RH
G_Acces_Finance
G_Acces_Direction
```

Ces groupes sont utilisés pour attribuer les permissions sur les ressources partagées.

Cette approche permet de gérer les accès via des groupes plutôt que directement sur les comptes utilisateurs.

### Avantages

- Administration simplifiée
- Gestion centralisée des droits
- Évolutivité
- Respect des bonnes pratiques Active Directory

## Authentification

Une fois connecté au domaine, un utilisateur peut ouvrir une session à l'aide de son compte Active Directory.

Exemple :

```text
LAB\mawountsac
```

L'authentification est vérifiée par le contrôleur de domaine DC01.

---

## Ordinateurs du domaine

Le poste suivant a été joint au domaine :

```text
DESKTOP-RNDT6FD
```

L'intégration au domaine permet :

- l'utilisation des comptes Active Directory ;
- l'application automatique des GPO ;
- la gestion centralisée des postes.

---

## Bénéfices de l'organisation retenue

Cette architecture permet :

- une administration centralisée ;
- une séparation logique des services ;
- une gestion simplifiée des permissions ;
- une application ciblée des stratégies de groupe ;
- une meilleure évolutivité de l'infrastructure.

---

## Compétences développées

À travers cette mise en œuvre, les compétences suivantes ont été acquises :

- Installation d'Active Directory Domain Services ;
- Promotion d'un serveur en contrôleur de domaine ;
- Gestion d'une forêt et d'un domaine ;
- Création et organisation des OU ;
- Création de comptes utilisateurs ;
- Jonction de postes au domaine ;
- Administration quotidienne d'Active Directory.
