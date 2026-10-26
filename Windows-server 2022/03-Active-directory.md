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

Afin de reproduire une organisation proche d'une PME, plusieurs unités d'organisation ont été créées.

### OU Utilisateurs

```text
OU Utilisateurs
│
├── IT
├── RH
├── Finance
└── Direction
```

Cette structure permet de séparer les utilisateurs par service et facilite l'application de stratégies spécifiques si nécessaire.

### OU Ordinateurs

```text
OU Ordinateurs
│
└── DESKTOP-RNDT6FD
```

Les postes du domaine sont regroupés dans cette unité d'organisation afin de faciliter leur administration.

---

## Utilisateurs créés

Plusieurs utilisateurs ont été créés afin de représenter différents services de l'entreprise.

| Service | Utilisateur |
|----------|-------------|
| IT | J. Awountsac |
| RH | A. Awountsac |
| Finance | M. Awountsac |
| Direction | U. Awountsac |

Chaque utilisateur dispose d'un compte distinct lui permettant de s'authentifier sur le domaine.

---

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
