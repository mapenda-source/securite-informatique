

### Travail Pratique sur le "SSH Tunneling et Proxying" sous Linux

#### 1. **Introduction**

- **Objectif :** Comprendre comment configurer et utiliser le tunneling SSH et le proxying pour une communication sécurisée.
- **Prérequis :** Connaissance de base des commandes Linux, SSH installé sur les machines client et serveur.

#### 2. **Préparation**

- **Configurer l'environnement :**
  - **Serveur :** Assurez-vous d'avoir accès à un serveur Linux distant avec SSH activé.
  - **Client :** Avoir une machine Linux à partir de laquelle vous allez initier le tunnel SSH.

#### 3. **Création d'un Tunnel SSH**

**Étape 1 : Configurer le Tunneling Local**

- **Description :** Le port forwarding local permet de transférer un port de votre machine locale vers un port sur un serveur distant.

- **Commande :**
  ```bash
  ssh -L port_local:hôte_cible:port_cible utilisateur@serveur_distant
  ```
  - `port_local` : Port sur votre machine locale (par exemple, `8080`).
  - `hôte_cible` : Nom d'hôte ou adresse IP du serveur cible auquel vous souhaitez accéder (par exemple, `localhost`).
  - `port_cible` : Port sur le serveur cible (par exemple, `80` pour HTTP).
  - `utilisateur` : Votre nom d'utilisateur SSH.
  - `serveur_distant` : Adresse du serveur distant.

- **Exemple :**
  ```bash
  ssh -L 8080:localhost:80 utilisateur@serveur-distant.com
  ```
  Cette commande transfère le port local 8080 vers le port 80 sur `serveur-distant.com`.

**Étape 2 : Tester le Port Forwarding Local**

- Ouvrez un navigateur web ou utilisez `curl` pour accéder au port transféré :
  ```bash
  curl http://localhost:8080
  ```
  Vous devriez voir la page web ou la réponse du serveur cible.

#### 4. **Port Forwarding Distant**

**Étape 1 : Configurer le Port Forwarding Distant**

- **Description :** Le port forwarding distant permet à un serveur distant de transférer un port vers une machine locale.

- **Commande :**
  ```bash
  ssh -R port_distant:hôte_local:port_local utilisateur@serveur_distant
  ```
  - `port_distant` : Port sur le serveur distant.
  - `hôte_local` : Adresse de la machine locale (par exemple, `localhost`).
  - `port_local` : Port sur votre machine locale.
  - `utilisateur` : Votre nom d'utilisateur SSH.
  - `serveur_distant` : Adresse du serveur distant.

- **Exemple :**
  ```bash
  ssh -R 9090:localhost:3000 utilisateur@serveur-distant.com
  ```
  Cela transfère le port 9090 sur `serveur-distant.com` vers le port 3000 sur votre machine locale.

**Étape 2 : Tester le Port Forwarding Distant**

- Accédez au port transféré depuis le serveur distant :
  ```bash
  curl http://localhost:9090
  ```
  Assurez-vous que le serveur distant peut atteindre votre service local fonctionnant sur le port 3000.

#### 5. **Port Forwarding Dynamique (Proxy SOCKS)**

**Étape 1 : Configurer le Port Forwarding Dynamique**

- **Description :** Le port forwarding dynamique permet de créer un serveur proxy SOCKS.

- **Commande :**
  ```bash
  ssh -D port_local utilisateur@serveur_distant
  ```
  - `port_local` : Port sur votre machine locale où le proxy SOCKS écoutera (par exemple, `1080`).
  - `utilisateur` : Votre nom d'utilisateur SSH.
  - `serveur_distant` : Adresse du serveur distant.

- **Exemple :**
  ```bash
  ssh -D 1080 utilisateur@serveur-distant.com
  ```

**Étape 2 : Configurer les Applications pour Utiliser le Proxy SOCKS**

- **Pour les Navigateurs Web :**
  - Accédez aux paramètres réseau et configurez les paramètres proxy pour utiliser `SOCKS5` avec `localhost` et le port `1080`.

- **Pour les Outils en Ligne de Commande :**
  - Vous pouvez utiliser des outils comme `curl` avec l'option `--proxy` :
    ```bash
    curl --proxy socks5h://localhost:1080 http://example.com
    ```

#### 6. **Dépannage**

- **Vérifiez les Logs SSH :** Consultez les journaux SSH sur le client et le serveur pour détecter les erreurs.
- **Vérifiez les Ports :** Utilisez des outils comme `netstat` ou `ss` pour vérifier si les ports sont correctement transférés.
- **Testez la Connectivité :** Assurez-vous que le serveur distant peut atteindre la machine locale et vice versa.

#### 7. **Conclusion**

- **Résumé :** Le tunneling et le proxying SSH sont des outils puissants pour sécuriser les communications réseau. Pratiquez l'utilisation du forwarding local, distant, et dynamique pour devenir compétent dans la gestion sécurisée du trafic réseau.
