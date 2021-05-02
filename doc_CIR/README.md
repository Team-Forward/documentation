
# 6 - Synthèse des travaux réalisés

### 6.1 - Indicateurs de recherche

Nos travaux de recherche ont été menés par des membres de l’équipe qui possèdent de fortes compétences non seulement en recherche, mais aussi dans les thématiques abordées. De plus, ont été encadrés par M. Julien Gossa en tant que professeur à l’UFR de Strasbourg.

  

Les expertises de notre équipe ont permis de définir, de piloter et de réaliser une démarche de recherche qui allie technique et technologie dans le but de réaliser ces opérations de preuve de concept sur nos outils.

Afin de mener au mieux ce projet, nous avons choisi de nous baser sur un fonctionnement incrémental du projet, découpé en trois versions différentes.

  

La première version contient l’essentiel de la fonctionnalité. Cette version contient le partage d’articles entre les utilisateurs présents sur le serveur Nextcloud. Le partage des différents articles via les réseaux sociaux a également été implémenté.

  

Une seconde version a été publiée. Cette version a consisté aux apports suivants :

-   Aperçu d’un article dans le corps du message lors du partage sur les réseaux sociaux.
    
-   Récupération des catégories depuis les flux RSS afin de les stocker.
    
-   Mise en place d’un importage automatique de hashtags à partir des catégories stockées pour un article.
    
-   Mise en place d’un système de flux par défaut dans la page de paramètres de l’application. Les flux sont définis par un administrateur du serveur Nextcloud. A chaque connexion d’un utilisateur, les flux par défaut sont ajoutés dans un dossier.
    

  

Une troisième et dernière version a été éditée. Cette version permet à l’administrateur d’ajouter des hashtags sur la page de paramètres de l’application. Lors du partage d’un article sur les réseaux sociaux, l’utilisateur choisit quels hashtags celui-ci souhaite importer dans le partage de l’article via un système de cases à cochées présent sur l’interface.

  

Comme le découpage en plusieurs versions précédemment évoqué l’atteste, nous avons suivi une méthode agile avec un découpage des tâches de travail en plusieurs sprints. Chacun de ces sprints contenait des objectifs précis avec une évaluation de ces derniers lors de la fin de la période. Ce fonctionnement nous a garanti une amélioration continue afin de maintenir le projet à un bon niveau de qualité.

Pour chaque version réalisée, des retours utilisateur ont été effectués afin de maintenir les évolutions dans la bonne direction.

Ces retours sont constitués de :

-   Démonstration des nouvelle évolutions
    
-   Prise de retours de l’utilisateur
    
-   Etablissement des prochains objectifs
    

  

Les processus décisionnels du projet ont été documentés. Chacune des décisions a été présentée et discutée au sein du groupe et, est retracée dans nos fichiers d’historique du projet.

### 6.2 - Synthèse des travaux réalisés

#### 6.2.1 - Partage entres utilisateurs

  

Afin d’obtenir les contacts présents sur le serveur avec lesquels nous pouvons partager les articles, il est nécessaire de l'interroger depuis la partie front-end.

L’implémentation actuelle de la partie front-end est implémentée en angularJS. Cette technologie est ancienne et n’a pas profité des dernières mises à jour de l’API Nextcloud. Nous avons alors été contraints d’utiliser une forme de l’API obsolète.

  

Il a été décidé de réaliser une duplication des articles à la place d’un référencement lors d’un partage d'articles. Cette solution a été retenue pour que l’utilisateur recevant l’article partagé dispose d’un contrôle total sur ce dernier. Ainsi, si l’utilisateur à l’origine du partage change l’état de l’article (passage à “vu” ou suppression par exemple), les modifications ne seront pas répercutées sur l’article qui a été partagé.

L’application ne comportait aucune fonctionnalité de partage avant la réalisation de ce projet. Dans la table stockant les différents articles de news, un champ contenant l’id de l’utilisateur ayant réalisé le partage a été ajouté.

Ainsi les articles ne comportant pas ce champ à null correspond aux articles qui ont été partagés.

  

Pour la répartition du code, l’architecture de l’application existante a été respectée et suivie scrupuleusement. Ainsi les modules du côté serveur ont été répartis de la manière suivante :

  

![](https://lh6.googleusercontent.com/kF_otuyeoiXl1FyS4O9XK_6eDPQTxH-Hjr4-8w3aFKdeQ088aDz9TnWo_VdO3uxZjGgWS6bRsIH6lihwBJvQ1cfatmHs7pBVcAEKejF4_jE5LpCfABcoA9IDeF2gu4hytZzKYWyD)

  

Voici les éléments mis à la disposition de l’utilisateur :

-   Icône de partage: Afin de partager un article, l’utilisateur accédera à un dropdown (énoncé ci-après) en cliquant sur l'icône de partage suivant <br>![](https://lh4.googleusercontent.com/ESY_DLnRhbke9L9gUkZz8_NZf-6yLygP2qZ5zECsnczlACFXLK7iy1-chAOYJ56UMvXlnv0CkpPzS6Lq2RLUDWEyy5zW_k6wqzQ6EmIrfPH1We3k5gd4vOr_bszAYD-5BuIIae8m)
    

Remarque: Cette icône appartient d’ailleurs à NextCloud, il a ainsi fallu uniquement provoquer son utilisation dans le CSS de la même manière que les autres icônes utilisées nativement.

-   Dropdown avec recherche d’utilisateurs :
    

![](https://lh3.googleusercontent.com/nj-Q3zLFQZ4zYgFoIWRVDOq1A2nhB-krtrFS9fvcHF2zP2qm0lKEkDzGmEozeaHFNeDo24nsgJs_0wp28kAujINuCoUAjTW317Z9Lm1TN-vJ60z8F_wW29RgCErNkp9IW_5QcGME)

-   [1] Input de recherche d’utilisateur
    

-   Champ de saisie pour rechercher un utilisateur destinataire du partage
    

-   [2] Indicateur de chargement
    

-   Indicateur qui révèle le chargement des requêtes, lié à la recherche des utilisateurs
    

-   [3] Hashtags pré-publication vers les réseaux sociaux
    

-   Checkbox donnant accès à d’autres checkboxes afin de proposer de multiples choix de hashtags intégrés au partage
    

-   [4] Boutons de partage vers les réseaux sociaux (FB, Twitter, email)
    

  

Afin d’intégrer le dropdown, il a fallu simplement ajouter un élément dans la page avec les sous-éléments précisés précédemment, adapter les composants afin de favoriser l’UX/UI, et améliorer l’ergonomie à travers le (CSS).

  

Exemple de procédé technique de recherche d’utilisateur:

-   Connexion du composant (<input>) avec le serveur (JS)
    
-   (Déclenchement de l’icône de chargement)
    
-   Traitement du serveur (récupération des utilisateurs, requête...)
    
-   Récupération des utilisateurs dans le front
    
-   (Désenclenchement de l’icône de chargement)
    
-   Affichage dans l'élément dropdown du résultat
    

  
  

-   Composants de configuration des flux par défaut, et des hashtags pré-définies :
    

  

![](https://lh4.googleusercontent.com/yVZnDM816wKFnfHlOrSpZQp-LuoGqE_rpTDpnAb86xCCoFtn-qAsREDxgzSiCPbjcHCsemuqD7sY0pcyNR9sFqTSxwEX3cK_g25lTlU6QOlDF_Ur42tFe-Jp2q9_9Okz02NL78Dk)

  

-   [1] Input de saisie URL du flux RSS
    

-   Champ de saisie pour définir un nouveau flux RSS (vérification de l’url post-saisie)
    

-   [2] Bouton de sauvegarde (va permettre de submit le formulaire au serveur)
    
-   [3] Élément récupéré/généré par le serveur, représentant le flux RSS
    
-   [4] Bouton de suppression
    

Les fonctionnalités implémentées ont entièrement été testées avec l’outil PHPUnit. Les tests rédigés ont été ajoutés à ceux déjà existants.

  

Ci-dessous une capture d’écran attestant que le code écrit lors de ce projet est couvert par des tests :

  

![](https://lh6.googleusercontent.com/hCQGMCeCMvsJh4H5tYzbVMcnTrTMsx6gyueaQZ2QhqllV4So5u66YqatIC0_WVkHvSOcMubzzGvhaVRFiV8BsQ-nIjD0OwLtBMH2mQuzg7tgLc_66IOZ7TviQFv7x9XrF2L8jJ-K)

  
  

#### 6.2.2 - Ajout de catégories sur les articles importés dans l’application

  

Afin de proposer un auto-import de hashtags, un champ stockant les catégories a été ajouté au modèle de données des articles. L’algorithme d’import des flux RSS a également été modifié pour que les catégories soient importées directement depuis le flux.

Les données sont stockées sous la syntaxe json car il est facile de manipuler ce format pour les parties back-end et front-end.

  

#### 6.2.3 - Ajout de flux par défaut

  

Les flux par défaut sont paramétrables uniquement par les administrateurs du serveur Nextcloud depuis la page “paramètres” de l’application news. Ce choix a été réalisé afin que la fonctionnalité proposée permette de partager des flux avec tous les utilisateurs du serveur.

Les flux sont stockés sous un format séréalisé dans la table des paramètres d’application.

Afin d’appliquer l’ajout du flux il était proposé deux choix :

-   Ajouter les flux pour tous les utilisateurs dès qu’un administrateur l’insert dans la page des paramètres. Cette option n’a pas été retenue car elle serait trop coûteuse en termes de ressource.
    
-   Ajouter les flux pour un utilisateur lors d’un événement de connexion survient. Cette solution a été choisie car elle permet de ne pas avoir de gaspillage de ressources pour les utilisateurs. De plus, aucune monopolisation des ressources du serveur n’est réalisée.
    

  

Pour réaliser une telle fonctionnalité, un module permettant la détection de connexion d’un utilisateur a été implémenté.

C’est à la connexion qu’il est vérifié si les flux par défaut sont présents dans le dossier de partage prévu à cet effet pour l’utilisateur. Si un des flux ou le dossier ne sont pas trouvés, ils sont créés pour l’utilisateur.

  

#### 6.2.4 - Ajout de hashtags par défaut

  

Afin de compléter l’import de hashtags, la conception d’une fonctionnalité de hashtags par défaut a été réalisée. Cette fonctionnalité permet aux administrateurs du serveur de proposer aux utilisateurs un lot de hashtags à placer de manière simple dans les partages sur les réseaux sociaux.

Les hashtags par défauts peuvent être ajoutés / modifiés uniquement par les administrateurs du serveur depuis la page de paramètres de l’application news.

Une fois qu’un hashtag a été ajouté, il est proposé depuis le menu créé pour le partage.

  

Pour implémenter cette fonctionnalité, il a été ajouté un champ dans la table des paramètres d’applications sous un format sérialisé. Ce champ contient tous les hashtags par défaut qui ont été ajoutés par un administrateur.

  

**Ajouter implémentation côté frontend.**
