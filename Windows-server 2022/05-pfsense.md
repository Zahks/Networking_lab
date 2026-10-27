# pfSense

## Présentation

pfSense est un pare-feu et routeur open source basé sur FreeBSD.

Dans ce laboratoire, il constitue le point central de la connectivité réseau.

Il assure :

- le routage entre le réseau interne et Internet ;
- la traduction d'adresses (NAT) ;
- la fonction de passerelle par défaut ;
- la sécurisation des flux réseau.

---

# Architecture réseau

## Interfaces

Le pare-feu dispose de deux interfaces réseau.

### WAN

L'interface WAN est connectée au réseau NAT VMware.

Configuration :

```text
Type : DHCP
Adresse : 192.168.80.137
Passerelle : 192.168.80.2
```

---

### LAN

L'interface LAN est utilisée par l'ensemble des équipements du domaine.

Configuration :

```text
Adresse : 192.168.1.1
Masque : 255.255.255.0
```

---

## Plan d'adressage

| Equipement | Adresse |
|------------|----------|
| VMware NAT Gateway | 192.168.80.2 |
| pfSense WAN | 192.168.80.137 |
| pfSense LAN | 192.168.1.1 |
| DC01 | 192.168.1.10 |
| Client Windows 11 | 192.168.1.100 |

---

# Rôle dans l'infrastructure

Le pare-feu est utilisé comme :

### Passerelle par défaut

Tous les postes du réseau utilisent :

```text
192.168.1.1
```

comme passerelle.

---

### Routeur

pfSense assure l'acheminement du trafic entre :

```text
192.168.1.0/24
```

et Internet.

---

### NAT

Les machines du réseau interne accèdent à Internet grâce à la traduction d'adresse réalisée par pfSense.

---

# Règles de filtrage

Une règle LAN autorise les équipements du réseau interne à accéder aux ressources externes.

Exemple :

```text
Default allow LAN to any rule
```

Cette règle autorise la communication depuis le réseau local vers toute destination.

---

# Incident majeur rencontré

## Symptômes

Après plusieurs semaines sans démarrer le laboratoire :

- les postes du domaine n'avaient plus accès à Internet ;
- la résolution DNS ne fonctionnait plus ;
- le serveur ne pouvait plus joindre Internet ;
- le diagnostic semblait indiquer plusieurs problèmes simultanés.

---

## Investigation

Plusieurs éléments ont été analysés :

### Routage

Vérification de la route par défaut :

```bash
route -n get default
```

---

### Connectivité WAN

Vérification de l'adresse WAN :

```bash
ifconfig em0
```

---

### Firewall

Contrôle des règles :

```bash
pfctl -sr
```

---

### NAT

Contrôle des règles NAT :

```bash
pfctl -sn
```

---

### DHCP WAN

Analyse du bail DHCP :

```bash
dhclient em0
```

---

## Première anomalie

Une passerelle incorrecte avait été enregistrée :

```text
192.168.1.50
```

comme passerelle par défaut.

Or cette adresse appartenait au réseau local.

La conséquence était la suivante :

```text
Clients LAN
        ↓
      pfSense
        ↓
    192.168.1.50
        ↓
      Échec
```

Le trafic Internet ne pouvait plus être routé correctement.

---

## Deuxième anomalie

L'interface WAN ne recevait plus d'adresse IPv4.

Conséquences :

```text
Pas d'adresse WAN
        ↓
Pas de passerelle WAN
        ↓
Pas de route par défaut
        ↓
Plus d'accès Internet
```

Le renouvellement du bail DHCP a permis de récupérer :

```text
192.168.80.137
```

sur l'interface WAN.

---

## Troisième anomalie

Malgré le retour de l'adresse WAN, les clients du réseau local restaient incapables d'accéder à Internet.

L'analyse de l'état des passerelles montrait :

```text
Status : Pending
```

---

## Cause identifiée

L'option suivante était activée sur l'interface WAN :

```text
Block private networks and loopback addresses
```

Le WAN étant connecté à un réseau VMware NAT :

```text
192.168.80.0/24
```

(considéré comme un réseau privé RFC1918),

pfSense considérait la passerelle WAN comme invalide.

---

## Résolution

L'option :

```text
Block private networks and loopback addresses
```

a été désactivée.

Après application de la configuration :

```text
Status : Online
```

est apparu pour la gateway WAN.

---

## Résultat

Les tests de connectivité ont confirmé :

- retour de l'accès Internet ;
- fonctionnement du routage ;
- fonctionnement du NAT ;
- fonctionnement de la résolution DNS.

L'infrastructure a retrouvé un fonctionnement normal.

---

# Enseignements tirés

Cet incident a permis de comprendre :

- le fonctionnement du routage sous pfSense ;
- le rôle des gateways ;
- le fonctionnement du NAT ;
- l'importance du DHCP WAN ;
- la différence entre WAN et LAN ;
- l'impact des réseaux privés RFC1918 dans pfSense ;
- les méthodes de diagnostic réseau utilisées en environnement professionnel.

---

# Compétences développées

- Installation et configuration de pfSense ;
- Configuration WAN/LAN ;
- Gestion des gateways ;
- Gestion du NAT ;
- Analyse du routage ;
- Diagnostic réseau ;
- Investigation d'incidents ;
- Dépannage de la connectivité Internet.
