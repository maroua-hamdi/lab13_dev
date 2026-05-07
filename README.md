<img width="313" height="605" alt="image" src="https://github.com/user-attachments/assets/03ff7784-26f8-4569-b2d0-71521c2ba677" /><img width="1310" height="604" alt="image" src="https://github.com/user-attachments/assets/fea9bb85-cd42-4448-99fe-421dfc25f549" /><img width="1722" height="389" alt="image" src="https://github.com/user-attachments/assets/8c6b5c80-2bd1-4946-9309-716bfadf64d1" /># Lab Android : Localisation GPS avec PHP, MySQL et OpenStreetMap

## 1. Présentation du projet

Ce lab consiste à développer une application Android permettant de récupérer la position GPS de l’utilisateur, d’enregistrer cette position dans une base de données MySQL grâce à un backend PHP, puis d’afficher les positions enregistrées sur une carte OpenStreetMap.

L’application utilise Android Studio pour la partie mobile, PHP pour le backend, MySQL pour la base de données, phpMyAdmin pour la gestion des données, et OSMDroid pour l’affichage de la carte.

---

## 2. Objectifs du lab

Les objectifs principaux de ce projet sont :

- Créer une application Android en Java.
- Demander l’autorisation d’accès à la localisation.
- Récupérer la latitude et la longitude de l’utilisateur.
- Envoyer les données GPS vers un serveur local PHP.
- Enregistrer les positions dans une base de données MySQL.
- Vérifier les données enregistrées avec phpMyAdmin.
- Afficher les positions sur une carte OpenStreetMap.
- Ajouter un marqueur sur la carte pour représenter la position enregistrée.

---

## 3. Technologies utilisées

- Android Studio
- Java
- XML
- PHP
- MySQL
- phpMyAdmin
- XAMPP
- Volley
- OSMDroid
- OpenStreetMap

---

## 4. Structure du backend PHP

La partie backend est placée dans le dossier `htdocs` de XAMPP.

Chemin utilisé :

`C:\xampp\htdocs\map_project`

Le dossier contient deux fichiers PHP :

- `createPosition.php`
- `getPositions.php`

`createPosition.php` permet d’enregistrer une nouvelle position dans la base de données.

`getPositions.php` permet de récupérer les positions enregistrées pour les afficher ensuite dans l’application Android.

### Capture 1 : dossier backend PHP


<img width="1722" height="389" alt="image" src="https://github.com/user-attachments/assets/f26b19eb-7d5e-4bd0-9a1b-b4f69c105264" />


---

## 5. Base de données MySQL

La base de données utilisée dans ce lab s’appelle :

`map_project`

Elle contient une table nommée :

`positions`

La table `positions` contient les champs suivants :

| Champ | Description |
|---|---|
| id | Identifiant unique de la position |
| latitude | Latitude récupérée depuis l’application |
| longitude | Longitude récupérée depuis l’application |
| date | Date et heure d’enregistrement |

Exemple de création de la table :

CREATE TABLE positions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    latitude DOUBLE NOT NULL,
    longitude DOUBLE NOT NULL,
    date DATETIME NOT NULL
);

---

## 6. Vérification de la table dans phpMyAdmin

Après la création de la base de données, on vérifie dans phpMyAdmin que la table `positions` existe bien dans la base `map_project`.

### Capture 2 : table dans phpMyAdmin



<img width="501" height="223" alt="image" src="https://github.com/user-attachments/assets/42a3c775-6ccb-4eae-a75b-ccdcd7c6ea12" />


Cette capture montre que la base de données `map_project` contient bien la table `positions`.

---

## 7. Demande d’autorisation de localisation

Au premier lancement de l’application, Android demande à l’utilisateur l’autorisation d’accéder à la localisation de l’appareil.

Cette autorisation est obligatoire pour permettre à l’application de récupérer la latitude et la longitude.

### Capture 3 : permission de localisation

<img width="303" height="603" alt="image" src="https://github.com/user-attachments/assets/7a8abfc5-fe2c-460c-bfde-f10f2ba03256" />


L’utilisateur doit cliquer sur :

`While using the app`

Cela autorise l’application à utiliser la localisation pendant son exécution.

---

## 8. Interface principale de l’application

Après l’acceptation de la permission, l’application affiche la position actuelle de l’utilisateur.

L’interface contient :

- la latitude ;
- la longitude ;
- un bouton pour enregistrer la position ;
- un bouton pour afficher la carte.

### Capture 4 : interface principale Android


<img width="300" height="606" alt="image" src="https://github.com/user-attachments/assets/fd356325-8721-4e01-ae18-c8056e7c8a46" />


Exemple de position affichée :

Latitude : 37.42199833333335  
Longitude : -122.084

Cette position correspond à la position récupérée depuis l’émulateur Android.

---

## 9. Enregistrement de la position

Lorsque l’utilisateur clique sur le bouton :

`Enregistrer ma position`

l’application envoie les données vers le fichier PHP :

`createPosition.php`

Les données envoyées sont :

- latitude ;
- longitude ;
- date.

Le serveur retourne ensuite une réponse JSON confirmant l’enregistrement.

Exemple de réponse :

{
  "success": true,
  "message": "Position enregistrée avec succès"
}

Cette réponse confirme que la communication entre Android, PHP et MySQL fonctionne correctement.

---

## 10. Vérification des positions enregistrées

Après l’enregistrement depuis l’application Android, on vérifie dans phpMyAdmin que les positions sont bien ajoutées dans la table `positions`.

### Capture 5 : positions enregistrées dans phpMyAdmin


<img width="1310" height="604" alt="image" src="https://github.com/user-attachments/assets/2b41496e-b328-414f-bb21-becca5a428c5" />


Dans cette capture, on peut voir plusieurs enregistrements contenant :

- un identifiant `id` ;
- une latitude ;
- une longitude ;
- une date d’enregistrement.

Cela prouve que l’application Android a bien envoyé les données vers la base MySQL.

---

## 11. Affichage de la carte OpenStreetMap

Après l’enregistrement de la position, l’utilisateur peut cliquer sur :

`Afficher la carte`

L’application ouvre alors une nouvelle activité contenant une carte OpenStreetMap.

Les positions enregistrées sont récupérées depuis le fichier :

`getPositions.php`

Ensuite, chaque position est affichée sur la carte avec un marqueur.

### Capture 6 : carte avec marqueur

<img width="313" height="605" alt="image" src="https://github.com/user-attachments/assets/8f0b6d90-79fa-488b-a46b-8c12ba54702a" />


Cette capture montre que la carte fonctionne correctement et que la position enregistrée est affichée avec un marqueur.

---

## 12. Fonctionnement général de l’application

Le fonctionnement global du lab est le suivant :

Application Android  
↓  
Récupération de la position GPS  
↓  
Affichage de la latitude et de la longitude  
↓  
Envoi des données vers le serveur PHP  
↓  
Traitement par `createPosition.php`  
↓  
Enregistrement dans la base MySQL  
↓  
Récupération avec `getPositions.php`  
↓  
Affichage des positions sur OpenStreetMap  

---

## 13. Fichiers principaux du projet Android

Les fichiers principaux de la partie Android sont :

- `MainActivity.java`
- `MapsActivity.java`
- `activity_main.xml`
- `activity_maps.xml`
- `AndroidManifest.xml`
- `network_security_config.xml`

Le fichier `MainActivity.java` permet de récupérer la position GPS et de l’envoyer vers le serveur PHP.

Le fichier `MapsActivity.java` permet d’afficher la carte et les marqueurs.

Le fichier `activity_main.xml` contient l’interface principale de l’application.

Le fichier `activity_maps.xml` contient la carte OpenStreetMap.

Le fichier `AndroidManifest.xml` contient les permissions nécessaires.

Le fichier `network_security_config.xml` permet d’autoriser les requêtes HTTP vers le serveur local.

---

## 14. Fichiers principaux du backend

Les fichiers principaux du backend sont :

- `createPosition.php`
- `getPositions.php`

### Rôle de `createPosition.php`

Ce fichier reçoit les données envoyées par l’application Android avec une requête POST.

Il reçoit :

- `latitude`
- `longitude`
- `date`

Ensuite, il insère ces données dans la table `positions`.

### Rôle de `getPositions.php`

Ce fichier récupère toutes les positions enregistrées dans la base de données.

Il retourne les résultats sous format JSON afin que l’application Android puisse les lire et les afficher sur la carte.

---

## 15. Résultat final

À la fin du lab, l’application permet de :

- demander l’autorisation de localisation ;
- récupérer la position GPS ;
- afficher la latitude et la longitude ;
- enregistrer la position dans MySQL ;
- vérifier les données dans phpMyAdmin ;
- afficher une carte OpenStreetMap ;
- afficher un marqueur sur la position enregistrée.

Les tests réalisés montrent que l’application fonctionne correctement.

---

## 16. Conclusion

Ce lab m’a permis de comprendre comment connecter une application Android à un backend PHP/MySQL.

J’ai appris à utiliser les permissions Android, à récupérer la localisation GPS, à envoyer des données vers un serveur local avec Volley, à stocker ces données dans une base MySQL, puis à afficher les positions sur une carte OpenStreetMap avec OSMDroid.

Le projet est fonctionnel, car les positions sont bien enregistrées dans phpMyAdmin et affichées correctement sur la carte avec un marqueur.
