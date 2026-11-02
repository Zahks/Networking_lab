# DNS et DHCP

## Présentation

Les services DNS et DHCP constituent deux éléments essentiels de toute infrastructure Microsoft.

Dans ce laboratoire, le DNS est hébergé sur le contrôleur de domaine DC01 tandis que la passerelle et le routage sont assurés par pfSense.

Ces services permettent aux machines du domaine de communiquer entre elles et de localiser les ressources Active Directory.

---

# DNS

## Rôle du DNS

Le DNS (Domain Name System) permet de traduire les noms en adresses IP.

Exemple :

```text
dc01.lab.local
```

peut être résolu vers :

```text
192.168.1.10
```

Dans un environnement Active Directory, le DNS est indispensable au fonctionnement du domaine.

Sans DNS fonctionnel :

- les utilisateurs ne peuvent pas s'authentifier ;
- les postes ne peuvent pas rejoindre le domaine ;
- les stratégies de groupe peuvent ne pas s'appliquer correctement.

---

## Serveur DNS

Le rôle DNS est installé sur :

```text
DC01
```

Adresse IP :

```text
192.168.1.10
```

Le DNS est intégré à Active Directory.

---

## Zone DNS

Zone configurée :

```text
lab.local
```

Cette zone contient notamment :

```text
dc01.lab.local
```

ainsi que les enregistrements nécessaires au fonctionnement d'Active Directory.

---

## Incident rencontré

Lors de la tentative de jonction du poste Windows 11 au domaine :

```text
lab.local
```

le message suivant est apparu :

```text
Impossible de contacter un contrôleur de domaine Active Directory.
```

---

## Diagnostic

Les vérifications ont montré que :

### Connectivité réseau

Le poste client pouvait joindre :

```text
192.168.1.10
```

par ping.

La connectivité IP fonctionnait donc correctement.

---

### Configuration DNS

Le poste Windows utilisait :

```text
192.168.1.1
```

comme serveur DNS.

Cette adresse correspond à pfSense.

---

## Cause

pfSense ne possède pas la zone :

```text
lab.local
```

Le client était donc incapable de résoudre :

```text
dc01.lab.local
```

et de localiser le contrôleur de domaine.

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

Après modification :

- le contrôleur de domaine a été localisé ;
- le poste a pu rejoindre le domaine ;
- l'authentification Active Directory est devenue fonctionnelle.

---

# DHCP

## Présentation

Le protocole DHCP (Dynamic Host Configuration Protocol) permet d'attribuer automatiquement des paramètres réseau aux postes clients.

Parmi ces paramètres :

- adresse IP ;
- masque ;
- passerelle ;
- serveur DNS.

---

## Architecture retenue

Dans le laboratoire, les adresses principales ont été configurées manuellement pour faciliter l'apprentissage du fonctionnement réseau.

Exemples :

| Machine | Adresse IP |
|----------|------------|
| pfSense | 192.168.1.1 |
| DC01 | 192.168.1.10 |
| Client Windows | 192.168.1.100 |

---

## Paramètres nécessaires à un poste du domaine

Pour fonctionner correctement, un poste du domaine doit disposer :

### Adresse IP

```text
192.168.1.x
```

---

### Passerelle

```text
192.168.1.1
```

(pfSense)

---

### DNS

```text
192.168.1.10
```

(DC01)

---

## Différence entre DNS et passerelle

Une erreur courante consiste à confondre ces deux paramètres.

### Passerelle

La passerelle permet d'accéder aux réseaux externes.

Dans ce laboratoire :

```text
192.168.1.1
```

---

### DNS

Le DNS permet de localiser les machines par leur nom.

Dans ce laboratoire :

```text
192.168.1.10
```

---

## Enseignements tirés

La mise en œuvre du domaine Active Directory a permis de comprendre que :

- un poste peut disposer d'une connectivité réseau fonctionnelle tout en étant incapable de rejoindre le domaine ;
- le DNS est un composant critique d'Active Directory ;
- la passerelle et le serveur DNS remplissent des rôles totalement différents ;
- la résolution de noms est souvent la première étape à vérifier lors des problèmes de jonction au domaine.

---

## Compétences développées

- Administration DNS sous Windows Server ;
- Compréhension des zones DNS ;
- Diagnostic de problèmes de résolution de noms ;
- Compréhension du rôle du DNS dans Active Directory ;
- Configuration IP manuelle ;
- Notions de DHCP ;
- Diagnostic de problèmes de jonction au domaine.
