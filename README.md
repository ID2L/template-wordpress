Voici un exemple de fichier `README.md` pour votre projet WordPress avec Docker :

---

# **Projet WordPress avec Docker**

Ce projet contient une configuration Docker pour déployer rapidement un site WordPress avec une base de données MySQL. Vous trouverez également un `.gitignore` pour versionner efficacement le code sans inclure les données sensibles ou inutiles.

---

## **Prérequis**

Avant de commencer, assurez-vous d’avoir installé sur votre machine :

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

### Étape 1 : Cloner le dépôt

Clonez ce projet sur votre machine locale :

```bash
git clone https://github.com/votre-utilisateur/votre-projet.git
cd votre-projet
```

### Étape 2 : Lancer les conteneurs

Démarrez les conteneurs Docker en exécutant la commande suivante :

```bash
docker-compose up -d
```

- Le conteneur WordPress sera accessible à l’adresse [http://localhost:8080](http://localhost:8080).
- Le conteneur MySQL est configuré pour stocker ses données dans `db_data`.

### Étape 3 : Configurer WordPress

1. Rendez-vous sur [http://localhost:8080](http://localhost:8080).
2. Suivez les étapes pour configurer WordPress :
   - Base de données :  
     - Hôte : `db`
     - Nom d’utilisateur : `wordpress`
     - Mot de passe : `wordpress`
     - Nom de la base : `wordpress`

### Étape 4 : Arrêter les conteneurs

Pour arrêter les conteneurs, utilisez la commande suivante :

```bash
docker-compose down
```

---

## **Sauvegarde et restauration**

### Sauvegarder les données

1. Sauvegardez les fichiers WordPress :
   ```bash
   tar -czf wordpress_data.tar.gz wordpress_data/
   ```

2. Sauvegardez la base de données MySQL :
   ```bash
   docker exec -it wordpress_db mysqldump -u root -p wordpress > wordpress.sql
   ```

### Restaurer les données

1. Extrayez les fichiers WordPress :
   ```bash
   tar -xzf wordpress_data.tar.gz -C wordpress_data/
   ```

2. Restaurez la base de données MySQL :
   ```bash
   docker exec -i wordpress_db mysql -u root -p wordpress < wordpress.sql
   ```

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

Si vous souhaitez contribuer à ce projet, n’hésitez pas à ouvrir une **issue** ou une **pull request**.

---

## **Licence**

Ce projet est sous licence MIT. Consultez le fichier `LICENSE` pour plus d’informations.

---