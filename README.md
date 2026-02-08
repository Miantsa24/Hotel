# Hotel Reservation System

Un système de réservation d'hôtels utilisant un framework web personnalisé en Java, avec une architecture MVC, base de données MySQL, et déploiement sur Tomcat.

## Fonctionnalités
- Affichage d'une liste d'hôtels.
- Formulaire de réservation avec validation.
- Sauvegarde des réservations en base de données.
- Framework personnalisé pour le mapping des routes et la gestion des vues.

## Technologies utilisées
- **Java 17** (obligatoire pour le framework).
- **Maven** pour la gestion des dépendances et le build.
- **Tomcat 10+** (Jakarta EE) pour le déploiement.
- **MySQL** pour la base de données.
- **JSP** pour les vues.

## Prérequis
1. **Java 17** : Téléchargez et installez JDK 17 (Oracle ou OpenJDK). Vérifiez avec `java -version`.
2. **Maven 3.6+** : Téléchargez depuis [maven.apache.org](https://maven.apache.org/download.cgi). Vérifiez avec `mvn -v`.
3. **Tomcat 10+** : Téléchargez depuis [tomcat.apache.org](https://tomcat.apache.org/download-10.cgi). Configurez `CATALINA_HOME`.
4. **MySQL 8+** : Installez MySQL Server. Créez une base `hotel_db` avec un user `root` (mot de passe `root` par défaut, modifiable dans `DatabaseConnection.java`).
5. **Git** : Pour cloner le repo.

## Installation et Configuration

### 1. Cloner le repository
```bash
git clone https://github.com/[votre-nouveau-repo].git
cd [nom-du-repo]
```

### 2. Configurer la base de données
- Démarrez MySQL.
- Exécutez le script SQL :
  ```bash
  mysql -u root -p < sql/init_database.sql
  ```
  (Entrez le mot de passe MySQL. Cela crée la DB `hotel_db` et insère des données de test.)

### 3. Construire le framework personnalisé
Le dossier `framework/` contient le code du framework. Si vous devez le mettre à jour :
- Clonez le repo du framework dans `framework/` (remplacez l'existant si nécessaire) :
  ```bash
  cd framework
  git clone https://github.com/Miantsa24/SPRINT1.git .
  ```
- Construisez le framework :
  ```bash
  ./build.bat  # Sur Windows
  # ou ./build.sh sur Linux/Mac
  ```
  Cela génère `monprojet.jar` dans `framework/` et le copie dans `src/main/webapp/WEB-INF/lib/`.

### 4. Construire et déployer l'application
- Retournez à la racine du projet :
  ```bash
  cd ..
  ```
- Construisez le WAR :
  ```bash
  set JAVA_HOME=C:\Program Files\Java\jdk-17  # Sur Windows
  mvn clean package
  ```
- Copiez le WAR généré (`target/hotel-app-1.0-SNAPSHOT.war`) vers le dossier `webapps` de Tomcat :
  - Arrêtez Tomcat.
  - Supprimez tout ancien déploiement (`hotel-app-1.0-SNAPSHOT.war` et dossier).
  - Copiez le nouveau WAR.
  - Redémarrez Tomcat.

### 5. Accéder à l'application
- Ouvrez un navigateur : `http://localhost:8080/hotel-app-1.0-SNAPSHOT/reservation/form`
- Testez le formulaire de réservation.

## Structure du projet
```
├── framework/              # Code du framework personnalisé
│   ├── src/                # Sources Java du framework
│   ├── build.bat/.sh       # Script de build du framework
│   └── ...
├── src/                    # Code de l'application principale
│   ├── main/
│   │   ├── java/
│   │   │   ├── controllers/  # Contrôleurs (MVC)
│   │   │   ├── dao/         # Accès base de données
│   │   │   └── models/      # Modèles
│   │   └── webapp/          # Ressources web (JSP, web.xml, lib/)
│   └── test/                # Tests (si présents)
├── sql/                    # Scripts SQL
├── pom.xml                 # Configuration Maven
└── README.md               # Ce fichier
```

## Développement
- **Branches** : Créez une branche pour chaque fonctionnalité (`git checkout -b feature/nom`).
- **Build** : `mvn clean compile` pour compiler sans WAR.
- **Tests** : Ajoutez des tests unitaires dans `src/test/`.
- **Pull Request** : Poussez votre branche et créez une PR pour review.

## Dépannage
- **Erreur 404** : Vérifiez que Tomcat est démarré et que le WAR est déployé. Consultez `logs/catalina.out`.
- **Erreur DB** : Vérifiez la connexion MySQL et les credentials dans `DatabaseConnection.java`.
- **Build échoue** : Assurez-vous que Java 17 est utilisé (`mvn -v` doit afficher Java 17).
- **Framework** : Si le framework ne scanne pas les contrôleurs, vérifiez que `monprojet.jar` est à jour dans `lib/`.

## Contributeurs
- [Votre nom] - Lead Developer
- Dev 1
- Dev 2

## Licence
Ce projet est sous licence MIT. Voir `LICENSE` pour plus de détails.