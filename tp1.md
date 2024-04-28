Voici un travail pratique sur la génération de clés SSH sous Linux. Ce travail peut être divisé en plusieurs étapes avec des objectifs précis pour chaque partie, permettant aux apprenants de comprendre comment créer, gérer et utiliser les clés SSH pour une connexion sécurisée.

### Objectif du travail pratique
Apprendre à générer, gérer et utiliser les clés SSH pour sécuriser les connexions entre machines sous Linux.

### Prérequis
- Accès à un terminal Linux.
- Compte utilisateur sur les machines Linux impliquées.

### Partie 1: Introduction aux Clés SSH
#### Objectifs:
- Comprendre le fonctionnement et l'importance des clés SSH.
- Savoir différencier clé publique et clé privée.

#### Questions:
1. Qu'est-ce qu'une clé SSH et pourquoi est-elle utilisée ?
2. Quelle est la différence entre une clé publique et une clé privée ?

### Partie 2: Génération de Clés SSH
#### Objectifs:
- Générer une paire de clés SSH (publique et privée).

#### Instructions:
1. Ouvrez votre terminal.
2. Tapez la commande suivante pour générer une paire de clés RSA:
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
3. Suivez les instructions à l'écran pour spécifier le fichier dans lequel sauvegarder les clés et entrer un mot de passe (facultatif mais recommandé pour plus de sécurité).

#### Questions:
1. Où sont stockées les clés générées par défaut sur votre système ?
2. À quoi sert le mot de passe que vous pouvez entrer lors de la génération des clés ?

### Partie 3: Transfert de la Clé Publique
#### Objectifs:
- Transférer la clé publique sur un serveur distant.

#### Instructions:
1. Utilisez la commande `ssh-copy-id` pour ajouter votre clé publique au serveur distant:
   ```bash
   ssh-copy-id utilisateur@adresse_du_serveur
   ```
2. Testez la connexion SSH au serveur sans entrer de mot de passe.

#### Questions:
1. Pourquoi est-il important de ne jamais transmettre votre clé privée ?
2. Que se passe-t-il si vous modifiez votre clé privée après avoir transféré votre clé publique ?

### Partie 4: Sécurisation de la Clé Privée
#### Objectifs:
- Comprendre et implémenter les mesures de sécurité pour protéger la clé privée.

#### Instructions:
1. Définissez les permissions appropriées pour votre fichier de clé privée:
   ```bash
   chmod 600 ~/.ssh/id_rsa
   ```
2. Réfléchissez à l'utilisation de phrases de passe complexes pour protéger votre clé.

#### Questions:
1. Quelles permissions avez-vous définies et pourquoi ?
2. Quel est l'avantage d'utiliser une phrase de passe pour votre clé privée ?

### Partie 5: Utilisation Pratique
#### Objectifs:
- Utiliser SSH pour se connecter à un serveur distant de manière sécurisée.

#### Instructions:
1. Connectez-vous au serveur distant en utilisant SSH:
   ```bash
   ssh utilisateur@adresse_du_serveur
   ```
2. Explorez les options avancées de SSH, comme le tunneling ou le transfert de port.

#### Questions:
1. Décrivez une situation où le tunneling SSH pourrait être utile.
2. Comment le transfert de port peut-il augmenter la sécurité des applications ?
