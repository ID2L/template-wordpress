# **Projet WordPress avec Docker**

Ce projet contient une configuration Docker pour déployer rapidement un site WordPress avec une base de données MySQL. Vous trouverez également un `.gitignore` pour versionner efficacement le code sans inclure les données sensibles ou inutiles.

---

## **Prérequis**

Avant de commencer, assurez-vous d'avoir installé sur votre machine :

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## **Structure du projet**

```plaintext
.
├── db_data                 # Données de la base MySQL (non versionnées)
├── wordpress_data          # Fichiers WordPress (wp-content, wp-admin, etc.)
├── docker-compose.yml      # Configuration Docker Compose
├── .gitignore              # Fichiers ignorés pour Git
└── README.md               # Ce fichier
```

---

## **Installation et utilisation**

### Étape 1 : Utiliser ce template

#### Option 1 : Via l'interface GitHub
1. Cliquez sur le bouton vert "Use this template"
2. Choisissez "Create a new repository"
   
Alternativement, vous pouvez cliquer sur "Download ZIP" pour télécharger le projet sans créer de dépôt.

#### Option 2 : Via ligne de commande (Linux)
```bash
wget https://github.com/ID2L/template-wordpress/archive/refs/heads/main.zip -O template.zip
unzip template.zip
mv votre-projet-main/* .
rm -rf votre-projet-main template.zip
```

Une fois le projet récupéré par l'une des deux méthodes, accédez au répertoire du projet :
```bash
cd votre-projet-main
```

### Étape 2 : Lancer les conteneurs

Démarrez les conteneurs Docker en exécutant la commande suivante :

```bash
docker-compose up -d
```

- Le conteneur WordPress sera accessible à l'adresse [http://localhost:8080](http://localhost:8080).
- Le conteneur MySQL est configuré pour stocker ses données dans `db_data`.

### Étape 3 : Configurer WordPress

1. Rendez-vous sur [http://localhost:8080](http://localhost:8080).
2. Suivez les étapes pour configurer WordPress :
   - Base de données :  
     - Hôte : `db`
     - Nom d'utilisateur : `wordpress`
     - Mot de passe : `wordpress`
     - Nom de la base : `wordpress`

### Étape 4 : Arrêter les conteneurs

Pour arrêter les conteneurs, utilisez la commande suivante :

```bash
docker-compose down
```

---

## **Sauvegarde et restauration**

La méthode recommandée pour sauvegarder et restaurer votre site WordPress est d'utiliser le plugin UpdraftPlus.

### Installation d'UpdraftPlus

1. Dans votre interface WordPress, allez dans "Extensions > Ajouter"
2. Recherchez "UpdraftPlus"
3. Cliquez sur "Installer maintenant" puis "Activer"

### Configuration pour un usage local

1. Accédez aux paramètres d'UpdraftPlus via "Réglages > UpdraftPlus Sauvegardes"
2. Dans l'onglet "Paramètres" :
   - Choisissez "Stockage local" comme destination de sauvegarde
   - Le dossier de sauvegarde par défaut sera `wordpress_data/wp-content/updraft/`

### Sauvegarder

1. Dans l'interface d'UpdraftPlus, cliquez sur "Sauvegarder maintenant"
2. Sélectionnez les éléments à sauvegarder :
   - Base de données
   - Plugins
   - Thèmes
   - Fichiers uploadés
   - Autres fichiers WordPress
3. Cliquez sur "Sauvegarder"

### Restaurer

1. Dans l'interface d'UpdraftPlus :
   - Soit importez une sauvegarde existante via "Charger une sauvegarde"
   - Soit sélectionnez une sauvegarde existante dans la liste
2. Cliquez sur "Restaurer"
3. Choisissez les composants à restaurer
4. Suivez les instructions à l'écran

### Note importante
Les sauvegardes sont stockées dans le dossier `wordpress_data/wp-content/updraft/`. Pour une sauvegarde complète de votre environnement, pensez à sauvegarder ce dossier en lieu sûr.

---

## **Personnalisation**

### Ports
Le port WordPress par défaut est `8080`. Pour le modifier, modifiez le fichier `docker-compose.yml` :

```yaml
ports:
  - "8080:80" # Remplacez 8080 par le port de votre choix
```

### Thèmes et plugins personnalisés
Ajoutez vos thèmes et plugins dans `wordpress_data/wp-content/themes` et `wordpress_data/wp-content/plugins`.

---

## **Dépannage**

### Le conteneur ne démarre pas
- Vérifiez que les ports ne sont pas déjà utilisés par une autre application.
- Assurez-vous que Docker est bien démarré.

### Réinitialiser la base de données
Pour réinitialiser la base de données MySQL, supprimez le dossier `db_data` :

```bash
rm -rf db_data/
docker-compose up -d
```

---

## **Contribution**

Si vous souhaitez contribuer à ce projet, n'hésitez pas à ouvrir une **issue** ou une **pull request**.

---

## **Licence**

Ce projet est sous licence MIT. Consultez le fichier `LICENSE` pour plus d'informations.

---