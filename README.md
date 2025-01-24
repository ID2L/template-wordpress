# **Projet WordPress avec Docker**

Ce projet contient une configuration Docker pour déployer rapidement un site WordPress avec une base de données MySQL.

---

## **Prérequis**

Avant de commencer, assurez-vous d'avoir installé sur votre machine :

- [Docker Desktop](https://www.docker.com/products/docker-desktop)

⚠️ **Important** : Docker Desktop doit être lancé et en cours d'exécution avant de commencer. Vous devriez voir l'icône Docker dans votre barre des tâches :
- Windows : 🐳 dans la barre des tâches
- Mac : 🐳 dans la barre de menu

---

## **Structure du projet**

```plaintext
.
├── docker-compose.yaml     # Configuration Docker Compose
├── extended_php.ini        # Configuration PHP personnalisée
├── .gitignore             # Fichiers ignorés pour Git
└── README.md              # Ce fichier
```

---

## **Installation et utilisation**

### Étape 1 : Télécharger le template

1. Cliquez sur le bouton vert "Code" en haut de cette page
2. Sélectionnez "Download ZIP"
3. Décompressez le fichier ZIP dans le dossier de votre choix
4. Renommez le dossier selon votre projet (exemple : `mon-site-wordpress`)

Résultat attendu après décompression :
```plaintext
mon-site-wordpress/
  ├── docker-compose.yaml
  ├── extended_php.ini
  ├── .gitignore
  └── README.md
```

### Étape 2 : Lancer les conteneurs

1. Ouvrez un terminal dans le dossier de votre projet
2. Exécutez la commande :

```bash
docker compose up -d
```

Vous devriez voir quelque chose comme :
```
[+] Running 3/3
 ✔ Network wordpress-setup_default  Created
 ✔ Container wordpress_db          Started
 ✔ Container wordpress            Started
```

### Étape 3 : Accéder à WordPress

1. Ouvrez votre navigateur
2. Accédez à [http://localhost:8080](http://localhost:8080)

Vous devriez voir l'écran d'installation de WordPress :
![Installation WordPress](https://example.com/wp-install.png)

### Étape 4 : Configurer WordPress

Remplissez les informations demandées :

1. Choisissez votre langue
2. Dans la page "Information nécessaires", utilisez :
   - Base de données : `wordpress`
   - Utilisateur : `wordpress`
   - Mot de passe : `wordpress`
   - Serveur de base de données : `db`
   - Préfixe des tables : `wp_` (laissez la valeur par défaut)

Résultat attendu : WordPress vous confirme que l'installation est réussie !

### Étape 5 : Arrêter les conteneurs

Quand vous avez terminé de travailler, dans le terminal :

```bash
docker compose down
```

Résultat attendu :
```
[+] Running 3/3
 ✔ Container wordpress      Stopped
 ✔ Container wordpress_db   Stopped
 ✔ Network wordpress_default  Removed
```

---

## **Utilisation quotidienne**

Pour démarrer votre environnement :
1. Lancez Docker Desktop
2. Attendez que l'icône 🐳 soit stable
3. Ouvrez un terminal dans le dossier de votre projet
4. `docker compose up -d`
5. Accédez à [http://localhost:8080](http://localhost:8080)

Pour arrêter votre environnement :
1. `docker compose down` dans le terminal
2. Vous pouvez fermer Docker Desktop si vous le souhaitez

---

## **Dépannage**

### Les conteneurs ne démarrent pas
1. Vérifiez que Docker Desktop est bien lancé (icône 🐳 stable)
2. Vérifiez qu'aucune autre application n'utilise le port 8080
3. Essayez de redémarrer Docker Desktop

### Page "Error establishing database connection"
1. Arrêtez les conteneurs : `docker compose down`
2. Relancez-les : `docker compose up -d`
3. Attendez 30 secondes que MySQL démarre complètement
4. Rafraîchissez la page

### Réinitialiser complètement
Si vous voulez tout recommencer à zéro :
```bash
docker compose down -v
docker compose up -d
```
⚠️ Attention : Cette commande supprimera toutes vos données !

---

## **Licence**

Ce projet est sous licence MIT. Consultez le fichier `LICENSE` pour plus d'informations.