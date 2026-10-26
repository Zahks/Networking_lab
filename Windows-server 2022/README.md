# Windows Server Lab

## Présentation

Ce projet a été réalisé dans le cadre d'un laboratoire personnel visant à développer des compétences en administration systèmes et réseaux.

L'objectif est de reproduire une infrastructure de type PME avec une gestion centralisée des utilisateurs, des postes et des ressources à l'aide de Windows Server, Active Directory et pfSense.

Ce laboratoire sert également de support d'apprentissage pour développer des compétences attendues sur des postes d'administrateur systèmes et réseaux.

---

## Objectifs du projet

- Déployer un contrôleur de domaine Active Directory
- Centraliser l'authentification des utilisateurs
- Gérer les ordinateurs du domaine
- Mettre en place des stratégies de groupe (GPO)
- Administrer des permissions NTFS
- Sécuriser l'accès aux ressources
- Déployer des applications par GPO
- Mettre en place un pare-feu pfSense
- Diagnostiquer et résoudre des incidents réseau

---

## Technologies utilisées

### Systèmes

- Windows Server 2022
- Windows 11
- pfSense

### Services

- Active Directory Domain Services (AD DS)
- DNS
- Group Policy Objects (GPO)
- Partages NTFS

### Virtualisation

- VMware Workstation

---

## Architecture

### Réseau

```text
Internet
    │
VMware NAT
    │
pfSense
WAN : 192.168.80.137
LAN : 192.168.1.1
    │
───────────────
Réseau 192.168.1.0/24
───────────────
    │
    ├── DC01
    │   192.168.1.10
    │
    └── DESKTOP-RNDT6FD
        192.168.1.100
```

---

## Active Directory

### Domaine

```text
lab.local
```

### Nom NetBIOS

```text
LAB
```

### Contrôleur de domaine

```text
DC01
```

---

## Structure Active Directory

### OU Utilisateurs

```text
OU Utilisateurs
│
├── Direction
|    └── U. Awountsac 
│
├── RH
│   └── A. Awountsac
│
├── Finance
│   └── M. Awountsac
│
└── IT
    └── U. Awountsac
```

### OU Ordinateurs

```text
OU Ordinateurs
│
└── DESKTOP-RNDT6FD
```

---

## Fonctionnalités mises en œuvre

### Gestion des utilisateurs

- Création de comptes utilisateurs
- Organisation par service
- Gestion des OU
- Authentification centralisée

### Gestion des ressources

- Création de partages réseau
- Gestion des permissions NTFS
- Gestion de l'héritage des autorisations

### Gestion des stratégies de groupe

- Fond d'écran d'entreprise
- Mappage de lecteurs réseau
- Redirection de dossiers
- Restrictions utilisateur
- Verrouillage automatique
- Politique de mot de passe complexe
- Déploiement MSI
- Désactivation de OneDrive
- Désactivation du Microsoft Store
- Blocage des périphériques USB

### Sécurité

- Pare-feu pfSense
- Contrôle des accès NTFS
- Gestion centralisée des stratégies de sécurité

---

## Incidents rencontrés et résolution

### Jonction impossible au domaine

Cause :

Le client utilisait pfSense comme serveur DNS.

Résolution :

Configuration du serveur DNS du client vers :

```text
192.168.1.10
```

---

### Déploiement MSI par GPO

Cause :

Filtrage de sécurité incomplet.

Résolution :

Ajout du groupe :

```text
Ordinateurs du domaine
```

avec les autorisations :

- Lecture
- Appliquer la stratégie de groupe

---

### Perte d'accès Internet

Causes :

- Mauvaise passerelle WAN
- Absence d'adresse WAN
- Option Block Private Networks activée sur un WAN VMware NAT

Résolution :

- Réattribution DHCP du WAN
- Vérification de la gateway par défaut
- Désactivation de Block Private Networks

Résultat :

Retour de la connectivité Internet pour l'ensemble du domaine.

---

## Compétences développées

### Windows Server

- Installation
- Configuration
- AD DS
- DNS

### Active Directory

- Gestion des utilisateurs
- Gestion des OU
- Gestion des ordinateurs
- Authentification

### GPO

- Déploiement logiciel
- Sécurisation des postes
- Gestion des utilisateurs

### Réseau

- Routage
- NAT
- DNS
- Pare-feu

### VMware

- Création de laboratoires virtualisés
- Gestion réseau NAT

### Dépannage

- Diagnostic DNS
- Diagnostic Active Directory
- Diagnostic GPO
- Diagnostic pfSense
- Diagnostic routage et NAT

---

## Évolutions prévues

- Supervision Zabbix
- LAPS
- PowerShell
- WSUS
- GLPI
- Microsoft 365
- Intune
