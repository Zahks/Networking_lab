# Contexte du projet

## Présentation

Ce projet a été réalisé dans le cadre d'un laboratoire personnel d'administration systèmes et réseaux.

L'objectif était de reproduire une infrastructure d'entreprise de type PME afin de développer des compétences pratiques sur les technologies couramment utilisées par les administrateurs systèmes.

L'environnement a été construit progressivement afin de comprendre la gestion centralisée des utilisateurs, des ordinateurs, des ressources partagées et de la sécurité dans un environnement Microsoft.

---

## Objectifs pédagogiques

Les principaux objectifs de ce projet étaient :

- Installer et administrer un contrôleur de domaine Windows Server ;
- Comprendre le fonctionnement d'Active Directory ;
- Gérer les utilisateurs, les groupes et les unités d'organisation (OU) ;
- Déployer et administrer des stratégies de groupe (GPO) ;
- Configurer des permissions NTFS et des partages réseau ;
- Mettre en place un pare-feu pfSense ;
- Comprendre les mécanismes DNS et DHCP ;
- Diagnostiquer des incidents systèmes et réseau ;
- Développer une méthodologie de documentation technique.

---

## Scénario retenu

L'infrastructure simule une petite entreprise composée de plusieurs services :

- Direction ;
- Ressources Humaines ;
- Finance ;
- Informatique.

Chaque service dispose de ses propres utilisateurs et de ressources dédiées.

L'objectif est de centraliser l'administration à l'aide d'Active Directory et d'appliquer des règles de sécurité cohérentes à l'ensemble des utilisateurs et des postes.

---

## Environnement technique

Le laboratoire a été déployé dans un environnement virtualisé.

### Infrastructure

- VMware Workstation ;
- pfSense ;
- Windows Server 2022 ;
- Windows 11.

### Réseau

Le réseau interne est organisé autour du sous-réseau :

```text
192.168.1.0/24
```

Le pare-feu pfSense assure :

- le routage ;
- le NAT ;
- l'accès Internet ;
- la sécurisation des flux.

---

## Organisation Active Directory

Le domaine Active Directory déployé est :

```text
lab.local
```

Le contrôleur de domaine principal est :

```text
DC01
```

L'organisation est structurée autour de plusieurs unités d'organisation (OU) représentant les services de l'entreprise.

### Utilisateurs

- J. Awountsac (IT)
- A. Awountsac (RH)
- M. Awountsac (Finance)
- U. Awountsac (Direction)

### Poste client

- DESKTOP-RNDT6FD

---

## Compétences visées

Ce projet a été conçu pour développer des compétences dans les domaines suivants :

### Administration Windows Server

- Installation et configuration ;
- Active Directory Domain Services ;
- DNS ;
- Authentification centralisée.

### Gestion des utilisateurs

- Création de comptes ;
- Gestion des OU ;
- Gestion des droits d'accès ;
- Gestion des groupes de sécurité.

### Gestion des postes

- Jonction au domaine ;
- Application de stratégies de groupe ;
- Déploiement logiciel.

### Réseau

- Adressage IP ;
- Routage ;
- NAT ;
- Pare-feu ;
- Dépannage réseau.

### Sécurité

- Politique de mot de passe ;
- Restriction des périphériques USB ;
- Désactivation de services non désirés ;
- Gestion des permissions NTFS.

---

## Démarche

L'approche retenue n'était pas uniquement de mettre en œuvre une infrastructure fonctionnelle mais également de comprendre les mécanismes internes des différents services.

Une attention particulière a été portée au diagnostic des incidents rencontrés lors du projet :

- problèmes DNS ;
- problèmes de jonction au domaine ;
- déploiement logiciel par GPO ;
- gestion des permissions NTFS ;
- dépannage pfSense ;
- dépannage du routage et de l'accès Internet.

Ces incidents ont permis de développer une méthodologie de résolution de problèmes proche de celle rencontrée en environnement professionnel.
