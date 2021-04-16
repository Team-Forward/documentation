<!-- # Documentation

Documentation for the share / default feeds features of the news app
Here's an other [page](guide.md ':include')
# Other things

> Here is an important thing to know about Docsify. 
* Making a list is easy
* Creating new items too !
* Just put a **\*** character at the beggining of the line !

# Getting started
1. To get started, you should get a **Nextcloud server** !<br>
1. After, you simply has to install **the news app**<br>
1. **Done !** -->

# A l'attention de Team-Forward
>Pour faire tourner cette page sur **docsify**, il faut run les commandes suivante :
```bash
npm i docsify-cli -g # Installation de docsify en global
docsify serve # Lancement du serveur en localhost
```

# Partage des articles présents dans News
**Fonctionnalité de partage entre les utilisateurs du serveur nextcloud ainsi que sur les réseaux sociaux.**
## Partage entre utilisateurs du serveur Nextcloud
### Fonctionnalité
L’application **News** ne comportait aucune fonctionnalité de partage avant la réalisation de ce projet. Il a été identifié le besoin de partager des articles entre utilisateur, la fonctionnalité présentée ci-dessous répond à ce besoin. 
### Interface
L'interface se présente de la manière suivante :<br>
![interface](/img/dropdown_nohashtags.png)
>L'utilisateur peut rechercher à l'aide de la **bare de recherche** un autre utilisateur pour lequel il veut envoyer un article.<br>Quand une requête de recherche est **en attente de réponse**, la recheche passe dans un état de **loading** (`isLoading = true`) et informe l'utilisateur que sa requête est en cours de traitement.  

Afin d’obtenir les contacts présents sur le serveur avec lesquels nous pouvons partager les articles, il est nécessaire de l'interroger depuis la partie front-end. 
L’implémentation actuelle de la partie front-end est implémentée en angularJS. Cette technologie est ancienne et n’a pas profité des dernières mises à jour de l’API Nextcloud. Nous avons alors été contraints d’utiliser une forme de l’API obsolète. 
### Stockage côté serveur
Dans la table stockant les différents articles de news, le champ suivant a été ajouté :
>**shared_by** : `string` avec valeur par défaut `null`. Le champ contient l’id de l’utilisateur ayant réalisé le partage. Ainsi les articles qui ne comportent pas ce champ à null correspond aux articles partagés.

### Implémentation
Il a été décidé de réaliser une **duplication des articles** à la place d’un référencement lors du partage d'un article. Cette solution a été retenue pour que l’utilisateur recevant l’article partagé dispose d’un contrôle total sur ce dernier. Ainsi, si l’utilisateur à l’origine du partage change l’état de l’article *(passage à “vu” ou suppression)*, les modifications ne seront pas répercutées sur l’article qui a été partagé. 

Côté **back-end**, voici l'architecture utilisée :<br><br>
![architecture-back-end](/img/architecture_back_end.png)<br>
>Le service `ShareService` a entièrement été crée. C'est ce service qui pourra intéragir avec le module `itemMapper` qui communique directement via les modèles avec la table `oc_news_item`. Le service comprend la méthode permettant de partager entre les utilisateur :
>```php
shareItemWithUser(string $userId, int $itemId, string $shareRecipientId) //Partage d'un article d'un utilisateur à l'autre

## Réseaux sociaux
### Fonctionnalité et réseaux disponibles 
Pour partager des articles avec des personnes n'étant pas forcément présentes sur le serveur Nextcloud, il a été intégré une fonctionnalitée de partage sur les réseaux sociaux à l'aide de **3 boutons**.<br>
[](#social-share)
![social-share-buttons](/img/social_share_buttons.png)
1. Partage sur **Facebook**.
1. Partage sur **Twitter**. 
1. Partage par **Mail**.

### Hashtags
Afin d'intégrer une intégration plus forte sur le partage des réseaux sociaux, des `hashtags` peuvent être ajoutés **manuellement** ou **automatiquement**.  
>Il est important de noter que sur **Facebook**, pour des raisons de limitations techniques du côté du réseau social, il n'est possible d'importer qu'**un seul hashtag**.   
#### Hashtags par défauts 
Comme le montre la capture [ci-dessus](/?id=fonctionnalité-et-réseaux-disponibles), **Les administrateurs** du serveur Nextcloud ont la possibilité d'**ajouter des hashtags** qui seront proposés **par défaut** lors d'un partage sur les réseaux sociaux. **L'utilisateur** choisi lors du partage les hashtags par défaut qu'**il a sélectionné**. 
#### Hashtags personnalisés
# Partage de feeds par défaut
## Fonctionnalité
## Interface administrateur 
## Interface utilisateur 
## Gestion côté serveur (event listener + paramètre dans table)
# Tests
# Pulls requests
