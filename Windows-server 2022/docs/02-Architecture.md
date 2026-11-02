# Architecture du laboratoire

## Vue d'ensemble

L'infrastructure a été conçue pour reproduire le fonctionnement d'une petite entreprise centralisant l'authentification, la gestion des ressources et l'administration des postes de travail.

L'architecture repose sur un pare-feu pfSense assurant le routage entre le réseau interne et Internet, un contrôleur de domaine Windows Server 2022 et un poste client Windows 11 joint au domaine.

---

## Schéma logique

```text
Internet
    │
VMware NAT
    │
WAN : 192.168.80.137
    │
┌───────────────┐
│    pfSense    │
│ LAN 192.168.1.1
└───────────────┘
    │
─────────────────────
Réseau 192.168.1.0/24
─────────────────────
    │
    ├── DC01
    │   192.168.1.10
    │
    └── DESKTOP-RNDT6FD
        192.168.1.100
```

---

## Infrastructure virtuelle

L'ensemble de l'environnement est exécuté sous VMware Workstation.

### Machines virtuelles

| Machine | Rôle |
|----------|--------|
| pfSense | Pare-feu, routing et NAT |
| DC01 | Contrôleur de domaine Active Directory |
| DESKTOP-RNDT6FD | Poste client Windows 11 |
| MON01 | Serveur Ubuntu destiné à la supervision Zabbix |

---

## Plan d'adressage

### Réseau WAN

Le WAN de pfSense est connecté au réseau NAT VMware.

| Equipement | Adresse |
|------------|----------|
| VMware NAT Gateway | 192.168.80.2 |
| pfSense WAN | 192.168.80.137 |

---

### Réseau LAN

Le réseau interne utilise le sous-réseau :

```text
192.168.1.0/24
```

| Equipement | Adresse |
|------------|----------|
| pfSense LAN | 192.168.1.1 |
| DC01 | 192.168.1.10 |
| Client Windows 11 | 192.168.1.100 |

---

## Contrôleur de domaine

### Nom du serveur

```text
DC01
```

### Adresse IP

```text
192.168.1.10
```

### Rôles installés

- Active Directory Domain Services (AD DS)
- DNS

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

---

## Services réseau

### DNS

Hébergé sur :

```text
DC01
192.168.1.10
```

Le service DNS est utilisé pour :

- la résolution du domaine ;
- l'authentification Active Directory ;
- la localisation du contrôleur de domaine.

---

### Routage

Le routage est assuré par :

```text
pfSense
```

La passerelle par défaut du réseau interne est :

```text
192.168.1.1
```

---

### NAT

Le NAT est assuré par pfSense.

Les postes du réseau interne accèdent à Internet par traduction d'adresse via l'interface WAN.

---

## Évolutions prévues

L'évolution de l'infrastructure prévoit l'ajout de nouveaux composants :

### Supervision

- Zabbix Server

### Administration

- PowerShell
- LAPS

### Gestion du parc

- GLPI

### Gestion des mises à jour

- WSUS

### Environnement hybride

- Microsoft 365
- Intune

### Caputure d'écrans 
- Schéma logique de l'architecture
- VMware avec les VM visibles
- Interfaces WAN/LAN de pfSense
- Configuration IP de DC01
  
