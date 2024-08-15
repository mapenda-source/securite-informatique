

### **TP : Surveillance de l'accès aux fichiers Linux avec auditd**

#### **Objectifs :**
- Comprendre le fonctionnement de `auditd` sur Linux.
- Configurer `auditd` pour surveiller les accès à des fichiers spécifiques.
- Analyser les logs générés par `auditd` pour détecter les activités suspectes.

#### **Prérequis :**
- Connaissance de base de la ligne de commande Linux.
- Connaissance des permissions des fichiers sous Linux.
- Accès à un système Linux avec les privilèges `root`.

#### **Matériel requis :**
- Un ordinateur avec une distribution Linux installée (par exemple, Ubuntu, Debian, CentOS).
- Accès à un terminal avec les privilèges `root`.

### **Partie 1 : Installation et configuration de `auditd`**

1. **Installer `auditd`:**
   - Ouvrez un terminal.
   - Installez le paquet `auditd` en utilisant le gestionnaire de paquets de votre distribution :
     ```bash
     sudo apt-get install auditd -y   # Pour Debian/Ubuntu
     sudo yum install audit -y        # Pour CentOS/RHEL
     ```

2. **Vérifier l’état du service `auditd`:**
   - Vérifiez si le service `auditd` est actif :
     ```bash
     sudo systemctl status auditd
     ```
   - Si le service n'est pas actif, démarrez-le :
     ```bash
     sudo systemctl start auditd
     ```
   - Assurez-vous que `auditd` démarre automatiquement au démarrage du système :
     ```bash
     sudo systemctl enable auditd
     ```

### **Partie 2 : Surveillance des accès à un fichier spécifique**

1. **Choisir un fichier à surveiller:**
   - Créez un fichier à surveiller (par exemple, `/etc/test_auditd.txt`):
     ```bash
     sudo touch /etc/test_auditd.txt
     ```
   - Modifiez les permissions du fichier pour permettre l'accès à des utilisateurs spécifiques, si nécessaire.

2. **Ajouter une règle d’audit pour surveiller les accès à ce fichier:**
   - Ajoutez une règle d’audit pour surveiller les accès en lecture (`read`) et en écriture (`write`) sur ce fichier :
     ```bash
     sudo auditctl -w /etc/test_auditd.txt -p rw -k test_auditd
     ```
   - Explication des options :
     - `-w /etc/test_auditd.txt` : Surveille ce fichier.
     - `-p rw` : Surveille les accès en lecture (`r`) et en écriture (`w`).
     - `-k test_auditd` : Tag pour identifier facilement les logs associés.

3. **Tester la règle d’audit:**
   - Accédez au fichier en tant qu'utilisateur normal ou modifiez-le pour générer des événements.
     ```bash
     cat /etc/test_auditd.txt
     echo "Test Audit" | sudo tee -a /etc/test_auditd.txt
     ```

### **Partie 3 : Analyse des logs générés par `auditd`**

1. **Afficher les logs générés par `auditd`:**
   - Utilisez la commande `ausearch` pour afficher les logs générés par `auditd` :
     ```bash
     sudo ausearch -k test_auditd
     ```

2. **Interpréter les résultats:**
   - Analysez les logs pour voir les détails de chaque accès au fichier, y compris l'utilisateur, l'heure, et le type d'accès (lecture, écriture, etc.).

3. **Exporter les logs pour un examen plus approfondi:**
   - Exportez les logs dans un fichier pour une analyse ou un rapport :
     ```bash
     sudo ausearch -k test_auditd > /tmp/auditd_logs.txt
     ```

### **Partie 4 : Nettoyage et conclusion**

1. **Supprimer la règle d’audit:**
   - Une fois les tests terminés, supprimez la règle d’audit pour éviter de générer des logs inutiles :
     ```bash
     sudo auditctl -W /etc/test_auditd.txt
     ```

2. **Désactiver `auditd` (facultatif):**
   - Si vous n’avez plus besoin de `auditd`, vous pouvez arrêter et désactiver le service :
     ```bash
     sudo systemctl stop auditd
     sudo systemctl disable auditd
     ```

3. **Conclusion:**
   - Discutez des cas d'utilisation de `auditd` dans un environnement de production, comme la surveillance des fichiers sensibles, la détection des intrusions, etc.

