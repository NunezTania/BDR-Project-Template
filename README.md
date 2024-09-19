# BDR-Project-Template

Une base de code pour les projets BDR

## Contenu

Ce repository contient un fichier docker-compose qui permet de monter une base de données PostgreSQL, en version 15, dans un container docker nommé ``bdr_project_db``. Vous pourrez communiquer avec ce container
depuis votre machine locale via le port 5444.
Vous trouverez également deux scripts SQL dans le dossier pgdata : 
- DDL.sql
- DML.sql

Le premier fichier contiendra la définition du schéma de votre base de données. Le deuxième contiendra l'insertion des tuples initialement présents dans votre base de données. Si vous modifier le nom du dossier contenant
ces scripts, veillez à le modifier également dans la définition du volume correspondant (lignes 16 et 35 du docker-compose).

## Puis-je modifier la configuration ou utiliser une autre configuration ?

Utiliser ce template n'est en aucun cas obligatoire, il permet simplement de normaliser les projets que vous rendrez. Il vous fournit également une base propre de développement si vous possédez
peu, voire aucune, expérience concernant les outils à utiliser dans le cadre de ce projet. Le fait de travailler avec des containers permet simplement d'éviter les problèmes de portage de votre projet
final, surtout si vous travailler dans un environnement différent de celui sur lequel nous effectueront les corrections finales. Notez que toutes modification du docker-compose aura un impact sur la
configuration de votre projet, qu'il s'agisse des ports, des réseau ou des noms de containers, faites donc bien attention à gérer toute modification que vous y apporterez.

## Comment utiliser ce template ?

Dans le docker-compose vous trouverez la définition de deux services :
- La base de données dans un container nommé ``db``
- L'application dans un container nommé ``app``

En plus de ces services, deux réseaux sont configurés pour permettre la communication entre les deux services et votre machine :
- frontend : qui permettra d'accéder à votre application depuis la machine locale
- backend : qui permettra au deux services de communiquer entre eux

Vous pourrez alors contacter votre base donnée depuis votre application via l'URL ``postgres://db:5432`` ou ``postgres://database:5432``. Cette communication aura lieu sur le réseau nommé ``backend``.
Pour accéder à votre application, utilisez l'url ``myapp:5454``. Si vous souhaitez changer le nom d'hôte, modifier l'attribut ``hostname`` du service ``app`` à la ligne 26 du docker-compose.

Pour lancer votre projet, vous n'aurez plus qu'à vous positionner à la racine de votre projet (vérifiez bien que le docker-compose y figure également) et exécuter la commande ``docker compose up``.
