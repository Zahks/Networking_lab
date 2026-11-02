# Group Policy Objects (GPO)

## Présentation

Les Group Policy Objects (GPO) permettent d'appliquer des paramètres de configuration et de sécurité aux utilisateurs et aux ordinateurs d'un domaine Active Directory.

Dans ce laboratoire, plusieurs GPO ont été mises en œuvre afin de reproduire des besoins couramment rencontrés en entreprise :

- standardisation des postes ;
- sécurisation des utilisateurs ;
- déploiement de ressources ;
- limitation de certaines fonctionnalités.

---

# Objectifs

Les principaux objectifs de cette partie du projet étaient :

- Comprendre le fonctionnement des GPO ;
- Administrer les postes de manière centralisée ;
- Automatiser certaines tâches ;
- Renforcer la sécurité des utilisateurs et des ordinateurs ;
- Découvrir la stratégie de groupe dans un environnement Active Directory.

---

# Fonctionnement des GPO

Les GPO sont stockées au niveau du domaine Active Directory.

Elles peuvent être appliquées :

- au domaine ;
- à une OU ;
- à un groupe d'utilisateurs ;
- à un groupe d'ordinateurs.

Les postes récupèrent automatiquement les stratégies lors de l'ouverture de session ou lors d'une actualisation des stratégies.

---

## Actualisation des stratégies

Pour forcer l'application immédiate d'une GPO :

```powershell
gpupdate /force
```

Cette commande a été utilisée à plusieurs reprises lors des phases de test.

---

# GPO déployées

## Fond d'écran d'entreprise

### Objectif

Uniformiser l'apparence des postes utilisateurs.

### Mise en œuvre

Le fond d'écran est stocké sur un partage réseau accessible en lecture seule.

### Résultat

Tous les utilisateurs reçoivent automatiquement le même fond d'écran lors de leur connexion.

### Compétences acquises

- Utilisation des chemins UNC ;
- Gestion des partages réseau ;
- Paramètres utilisateur.

---

## Mappage des lecteurs réseau

### Objectif

Fournir automatiquement l'accès aux ressources partagées.

### Résultat

Les lecteurs réseau apparaissent automatiquement pour les utilisateurs concernés.

### Compétences acquises

- Préférences GPO ;
- Gestion des ressources réseau ;
- Centralisation des accès.

---

## Redirection de dossiers

### Objectif

Centraliser les données utilisateurs sur le serveur.

### Dossiers concernés

- Documents
- Bureau

### Résultat

Les données sont stockées sur le serveur plutôt que localement.

### Compétences acquises

- Gestion des profils utilisateurs ;
- Stockage centralisé ;
- Disponibilité des données.

---

## Restrictions utilisateur

### Objectif

Limiter certaines actions sur les postes de travail.

### Exemples

- Limitation de fonctionnalités système ;
- Restriction d'accès à certains paramètres Windows.

### Compétences acquises

- Gestion des paramètres utilisateur ;
- Durcissement de l'environnement Windows.

---

## Verrouillage automatique de session

### Objectif

Renforcer la sécurité des postes laissés sans surveillance.

### Résultat

Le poste se verrouille automatiquement après une période d'inactivité définie.

### Compétences acquises

- Gestion de la sécurité utilisateur ;
- Politiques de session.

---

## Politique de mot de passe complexe

### Objectif

Améliorer la sécurité des comptes Active Directory.

### Paramètres

- Complexité activée ;
- Longueur minimale ;
- Historique de mots de passe.

### Résultat

Les utilisateurs doivent respecter des règles de sécurité lors du choix de leur mot de passe.

### Compétences acquises

- Sécurité Active Directory ;
- Gestion des comptes utilisateurs.

---

## Déploiement d'applications MSI

### Objectif

Installer automatiquement un logiciel sur les postes du domaine.

### Configuration

Le déploiement est réalisé via un paquet MSI.

### Difficulté rencontrée

Le déploiement ne fonctionnait pas initialement.

### Cause

Les autorisations nécessaires n'étaient pas appliquées au groupe :

```text
Ordinateurs du domaine
```

### Résolution

Ajout des droits :

- Lecture ;
- Appliquer la stratégie de groupe.

### Compétences acquises

- Déploiement logiciel centralisé ;
- Dépannage GPO ;
- Gestion des autorisations.

---

## Désactivation de OneDrive

### Objectif

Empêcher l'utilisation de OneDrive dans l'environnement du laboratoire.

### Résultat

Le service OneDrive devient indisponible pour les utilisateurs.

### Compétences acquises

- Gestion des composants Windows ;
- Contrôle des services cloud.

---

## Désactivation du Microsoft Store

### Objectif

Limiter l'installation libre d'applications.

### Résultat

Les utilisateurs ne peuvent plus utiliser le Microsoft Store.

### Compétences acquises

- Contrôle des applications ;
- Politique de sécurité poste.

---

## Blocage des périphériques USB

### Objectif

Limiter les risques de fuite ou d'introduction de données.

### Résultat

Les périphériques de stockage USB sont bloqués.

### Compétences acquises

- Sécurisation des postes ;
- Gestion des périphériques ;
- Politique de sécurité.

---

# Validation

L'ensemble des stratégies a été testé depuis le poste :

```text
DESKTOP-RNDT6FD
```

Les tests ont permis de vérifier :

- l'application correcte des GPO ;
- la réplication des paramètres ;
- le comportement attendu des utilisateurs.

---

# Difficultés rencontrées

## Déploiement MSI

L'installation automatisée d'un logiciel via GPO a nécessité plusieurs phases de diagnostic.

L'analyse des autorisations de sécurité de la stratégie a permis d'identifier l'origine du problème.

Cette étape a fortement contribué à la compréhension du mécanisme de filtrage des stratégies de groupe.

---

# Intérêt en entreprise

Les GPO permettent de :

- standardiser les postes ;
- renforcer la sécurité ;
- réduire les tâches manuelles ;
- déployer des ressources à grande échelle ;
- appliquer des règles homogènes sur l'ensemble du domaine.

---

# Compétences développées

- Administration des GPO ;
- Sécurité Windows ;
- Déploiement logiciel ;
- Gestion des profils utilisateurs ;
- Gestion des ressources réseau ;
- Diagnostic de problèmes GPO ;
- Application de stratégies centralisées.
