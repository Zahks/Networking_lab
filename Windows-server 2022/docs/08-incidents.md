# Incident 001 - Perte du mot de passe Ubuntu Server

## Symptôme

Impossible de se connecter au serveur Ubuntu après l'installation.

Les tentatives de connexion renvoyaient systématiquement :

```text
Login incorrect
```

---

## Analyse

Plusieurs hypothèses ont été envisagées :

- erreur sur le mot de passe ;
- erreur sur le nom d'utilisateur ;
- problème de configuration clavier ;
- problème système.

L'accès à la machine était totalement bloqué.

---

## Cause

Le mot de passe utilisateur défini lors de l'installation n'était plus connu avec certitude.

L'absence d'affichage des caractères lors de la saisie compliquait le diagnostic.

---

## Résolution

Accès au menu GRUB.

Démarrage du mode Recovery.

Passage en shell root puis exécution des commandes :

```bash
mount -o remount,rw /
passwd florin
```

Définition d'un nouveau mot de passe.

---

## Résultat

Le serveur est redevenu accessible sans nécessiter de réinstallation.

---

# Incident 002 - Problème de disposition clavier sous Ubuntu

## Symptôme

Certaines commandes et mots de passe semblaient incorrects malgré une saisie apparemment correcte.

La saisie de caractères spéciaux produisait des résultats inattendus.

---

## Analyse

Plusieurs caractères ne correspondaient pas aux touches utilisées sur le clavier physique.

Les caractères suivants étaient particulièrement concernés :

```text
!
@
/
:
```

---

## Cause

La disposition clavier configurée sur Ubuntu ne correspondait pas à la disposition utilisée sur le poste de travail.

Le système n'était pas configuré en :

```text
French (AZERTY)
```

---

## Résolution

Reconfiguration du clavier système :

```bash
sudo dpkg-reconfigure keyboard-configuration
```

Choix de :

```text
French (AZERTY)
```

puis application de la nouvelle configuration.

---

## Résultat

Les caractères spéciaux ont retrouvé le comportement attendu.

Les commandes et mots de passe pouvaient être saisis correctement.

---

# Incidents rencontrés

## Présentation

Tout au long du projet, plusieurs incidents techniques ont été rencontrés.

Cette section présente les principales difficultés rencontrées, les méthodes de diagnostic utilisées et les solutions apportées.

Ces incidents ont permis de développer des compétences pratiques en dépannage système et réseau.

---

# Incident 003 - Impossible de joindre le domaine

## Symptôme

Lors de la tentative de jonction du poste Windows 11 au domaine :

```text
lab.local
```

le message suivant apparaissait :

```text
Impossible de contacter un contrôleur de domaine Active Directory.
```

---

## Analyse

Les tests de connectivité ont confirmé que :

```text
192.168.1.10
```

(le contrôleur de domaine) répondait correctement au ping.

Le problème ne concernait donc pas la connectivité réseau.

---

## Cause

Le poste Windows utilisait :

```text
192.168.1.1
```

(pfSense)

comme serveur DNS.

Or pfSense ne connaissait pas le domaine :

```text
lab.local
```

---

## Résolution

Le DNS du poste client a été modifié :

Avant :

```text
192.168.1.1
```

Après :

```text
192.168.1.10
```

---

## Résultat

Le poste a immédiatement pu rejoindre le domaine Active Directory.

---

# Incident 004 - Déploiement MSI par GPO impossible

## Symptôme

Le logiciel déployé via GPO ne s'installait pas automatiquement sur le poste client.

---

## Analyse

La GPO était correctement configurée.

Le partage réseau contenant le package MSI était accessible.

---

## Cause

Les autorisations de sécurité de la GPO n'étaient pas suffisantes.

Le groupe :

```text
Ordinateurs du domaine
```

ne disposait pas des droits nécessaires.

---

## Résolution

Ajout des autorisations :

- Lecture ;
- Appliquer la stratégie de groupe.

---

## Résultat

Le déploiement MSI a fonctionné correctement lors du redémarrage du poste.

---

# Incident 005 - Compréhension des permissions NTFS

## Symptôme

Les résultats obtenus ne correspondaient pas toujours aux permissions attendues.

Certains utilisateurs disposaient encore de droits non désirés.

---

## Analyse

Les permissions héritées continuaient à être appliquées.

---

## Cause

Les dossiers héritaient des autorisations du dossier parent.

---

## Résolution

Désactivation sélective de l'héritage NTFS.

Suppression des autorisations inutiles.

Création de permissions explicites basées sur les groupes de sécurité.

---

## Résultat

Les accès sont devenus cohérents et plus simples à administrer.

---

# Incident 006 - Perte totale d'accès Internet

## Symptôme

Après plusieurs semaines sans démarrer le laboratoire :

- plus d'accès Internet ;
- impossibilité de résoudre des noms ;
- impossibilité d'accéder à certaines ressources réseau.

---

## Analyse

Les vérifications suivantes ont été réalisées :

```bash
ping
tracert
route -n get default
ifconfig
dhclient
pfctl -sr
pfctl -sn
```

---

## Cause n°1

Une passerelle incorrecte était définie :

```text
192.168.1.50
```

comme passerelle par défaut.

Cette adresse appartenait au réseau local et non au réseau WAN.

---

## Correction

Remplacement de la passerelle incorrecte par la passerelle DHCP du réseau VMware NAT.

---

# Incident 007 - Absence d'adresse sur l'interface WAN

## Symptôme

La commande :

```bash
ifconfig em0
```

ne retournait aucune adresse IPv4.

---

## Analyse

Le WAN ne recevait plus de bail DHCP.

---

## Résolution

Renouvellement manuel du bail :

```bash
dhclient em0
```

---

## Résultat

Le WAN a récupéré :

```text
192.168.80.137
```

---

# Incident 007 - Gateway WAN en état "Pending"

## Symptôme

Dans l'interface pfSense :

```text
Status → Gateways
```

la passerelle WAN apparaissait :

```text
Pending
```

---

## Conséquence

Le WAN semblait fonctionner alors que les équipements du LAN restaient incapables d'accéder à Internet.

---

## Analyse

Les tests ont montré que :

- Ping WAN → Internet : OK
- Ping LAN → Internet : KO

---

## Cause

L'option suivante était activée :

```text
Block private networks and loopback addresses
```

sur l'interface WAN.

Le WAN était connecté à un réseau VMware NAT :

```text
192.168.80.0/24
```

qui est considéré comme un réseau privé.

pfSense refusait donc de considérer la gateway comme valide.

---

## Résolution

Désactivation de :

```text
Block private networks and loopback addresses
```

sur l'interface WAN.

---

## Résultat

La gateway est passée :

```text
Pending
↓
Online
```

et la connectivité Internet est revenue pour l'ensemble du laboratoire.

---

# Enseignements tirés

Ces incidents ont permis de développer :

- une méthodologie de diagnostic ;
- une meilleure compréhension de DNS ;
- une meilleure compréhension de NAT ;
- une meilleure compréhension du routage ;
- la maîtrise des outils de diagnostic réseau ;
- la résolution de problèmes Active Directory ;
- l'analyse des permissions NTFS ;
- le dépannage d'une infrastructure pfSense.
- Utilisation du mode Recovery Ubuntu ;
- Réinitialisation d'un mot de passe Linux ;
- Compréhension du processus de démarrage Linux ;
- Administration de base d'Ubuntu Server.
---

# Compétences développées grâce aux incidents

- Diagnostic DNS ;
- Diagnostic Active Directory ;
- Diagnostic GPO ;
- Diagnostic NTFS ;
- Diagnostic réseau ;
- Routage ;
- NAT ;
- pfSense ;
- Résolution méthodique d'incidents.
- Configuration du clavier sous Linux ;
- Diagnostic des problèmes liés à la disposition clavier ;
- Administration de base d'Ubuntu Server ;
- Dépannage système.
