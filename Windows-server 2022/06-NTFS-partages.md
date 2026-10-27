# Permissions NTFS et partages réseau

## Présentation

Afin de reproduire un environnement d'entreprise réaliste, plusieurs ressources partagées ont été mises en place sur le serveur.

Chaque service de l'entreprise dispose de son propre espace de stockage afin de garantir la confidentialité et l'intégrité des données.

La gestion des accès repose sur :

- les groupes Active Directory ;
- les permissions NTFS ;
- les partages réseau Windows.

---

# Objectifs

Cette partie du projet avait pour objectifs de :

- comprendre les permissions NTFS ;
- comprendre la différence entre partage et NTFS ;
- mettre en œuvre un contrôle d'accès basé sur les groupes ;
- appliquer le principe du moindre privilège ;
- sécuriser les données des différents services.

---

# Ressources partagées

Les dossiers suivants ont été créés :

```text
Finance
RH
IT
Direction
```

Chaque dossier correspond à un service spécifique de l'entreprise.

---

# Organisation des groupes

Afin de simplifier l'administration des permissions, plusieurs groupes de sécurité Active Directory ont été créés.

## Groupes métiers

```text
G_IT
G_RH
G_Finance
G_Direction
```

Ces groupes regroupent les utilisateurs selon leur service.

Exemple :

```text
Mariola Awountsac
    ↓
G_Finance
```

---

## Groupes d'accès

```text
G_Acces_IT
G_Acces_RH
G_Acces_Finance
G_Acces_Direction
```

Ces groupes sont utilisés pour attribuer les permissions sur les ressources partagées.

---

# Modèle d'attribution des permissions

L'attribution des accès repose sur une approche utilisant les groupes plutôt que les utilisateurs individuels.

Principe :

```text
Utilisateur
        ↓
 Groupe métier
        ↓
 Groupe d'accès
        ↓
 Ressource
```

Exemple :

```text
M. Awountsac
        ↓
      G_Finance
        ↓
  G_Acces_Finance
        ↓
 Dossier Finance
```

Cette approche simplifie fortement l'administration.

---

# Permissions NTFS

Les autorisations sont attribuées aux groupes de sécurité.

Exemple :

## Dossier Finance

```text
G_Acces_Finance
    Lecture
    Écriture

Autres groupes
    Aucun accès
```

---

## Dossier RH

```text
G_Acces_RH
    Lecture
    Écriture

Autres groupes
    Aucun accès
```

---

## Dossier IT

```text
G_Acces_IT
    Lecture
    Écriture

Autres groupes
    Aucun accès
```

---

## Dossier Direction

```text
G_Acces_Direction
    Lecture
    Écriture

Autres groupes
    Aucun accès
```

---

# Héritage NTFS

## Principe

Par défaut, les dossiers héritent des autorisations de leur dossier parent.

Exemple :

```text
D:\Partages
│
├── Finance
├── RH
├── IT
└── Direction
```

Les permissions appliquées sur :

```text
Partages
```

peuvent être automatiquement héritées par les sous-dossiers.

---

## Problème rencontré

Lors de la mise en place des permissions, certaines autorisations héritées accordaient des accès non souhaités.

La gestion des droits devenait difficile à contrôler.

---

## Solution mise en œuvre

L'héritage a été désactivé sur certains dossiers afin de :

- supprimer les permissions inutiles ;
- conserver uniquement les groupes nécessaires ;
- simplifier l'analyse des droits.

Cette manipulation a permis d'appliquer des permissions explicites plus précises.

---

# Permissions explicites et héritées

Au cours du projet, plusieurs notions importantes ont été étudiées.

## Permissions explicites

Elles sont définies directement sur une ressource.

Exemple :

```text
G_Acces_Finance
→ Lecture / Écriture
```

sur le dossier Finance.

---

## Permissions héritées

Elles proviennent d'un dossier parent.

Exemple :

```text
Partages
    ↓
Finance
```

Les autorisations appliquées sur :

```text
Partages
```

peuvent être transmises automatiquement aux sous-dossiers.

---

## Refus explicite

Une autorisation de type :

```text
Refuser
```

est prioritaire sur les autorisations de type :

```text
Autoriser
```

Cette notion a permis de comprendre l'ordre de traitement des permissions NTFS.

---

# Différence entre partage et NTFS

Deux niveaux de sécurité interviennent lors de l'accès à une ressource réseau.

## Permissions de partage

Elles contrôlent l'accès au partage.

Exemple :

```text
\\DC01\Finance
```

---

## Permissions NTFS

Elles contrôlent l'accès réel aux fichiers et aux dossiers.

---

## Permissions effectives

L'autorisation finale obtenue par un utilisateur est le résultat de la combinaison :

```text
Permissions de partage
+
Permissions NTFS
```

Le niveau le plus restrictif est appliqué.

---

# Validation

Des tests ont été réalisés avec plusieurs comptes utilisateurs afin de vérifier :

- l'accès autorisé au dossier du service concerné ;
- l'absence d'accès aux autres dossiers ;
- la cohérence des groupes de sécurité.

Les résultats ont confirmé le bon fonctionnement des permissions mises en œuvre.

---

# Compétences développées

- Gestion des permissions NTFS ;
- Gestion des groupes Active Directory ;
- Utilisation des groupes de sécurité ;
- Gestion de l'héritage ;
- Permissions explicites et héritées ;
- Contrôle d'accès basé sur les rôles ;
- Administration des partages réseau ;
- Application du principe du moindre privilège.
