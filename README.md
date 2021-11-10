# Points d'Intérêts à Lyon

# Sommaire:

1. Contexte
2. Planning
3. Analyses des données brutes
4. Méthodes utilisées : Text mining - Géographie/Clustering
5. Conclusions

# CONTEXTE:

Après réception du cahier des charges et acceptation de celui-ci, notre équipe est fière de vous présenter le travail réalisé répondant à votre demande.

Dans une optique d'amélioration d'une prise en charge des lieux touristiques à Lyon notamment via les transports en commun, une étude sur les données des photos prises a été commanditée.

Votre société nous a demandé une analyse sur une extraction d'une base de données Flickr.

Pour rappel nous trouverons ci-dessous l'historique de nos échanges ainsi que le détail de la mission et la répartition des tâches entre nos 2 sociétés dénommées (Client: AlisonPatou - Prestataire : Adil-Nasreddine):

- Fourniture d'un jeu de données sous format csv : Client
- Définition des livrables : Client
    - Rapport écrit contenant: contexte, planning, analyses et recommandations
    - Notebook contenant : les analyses
- Fourniture des livrables cités ci-dessus : Prestataire

Les outils utilisés afin de mener cette étude sont les suivants :

- Jupyter Notebook : Code, analyse et résultat.
- [Notion.so](http://Notion.so) : Planning et rédaction du rapport.

# PLANNING:

Nous trouverons ci-dessous le planning suivi des différentes tâches à réaliser afin de livrer le projet pour le 10/11 à 12H00:

Jour 1 : Prise de connaissance du projet et du jeu de données

Jour 2 : Analyses géographique et text mining

Jour 3 :  Rédaction du rapport et finalisation

# Analyses des données brutes

Le fichier brut fourni par le Client est sous format .csv de 10Mo contenant les données suivantes :

```
 #   Colonnes            Nombre valeurs  Type de valeurs
---  ------              --------------  -----
 0   id                  83837 non-null  int64*
 1   user                83837 non-null  object*
 2   lat                 83837 non-null  float64*
 3   long                83837 non-null  float64
 4   tags                72076 non-null  object
 5   title               79009 non-null  object
 6   date_taken_minute   83837 non-null  int64
 7   date_taken_hour     83837 non-null  int64
 8   date_taken_day      83837 non-null  int64
 9   date_taken_month    83837 non-null  int64
 10  date_taken_year     83837 non-null  int64
 11  date_upload_minute  83837 non-null  int64
 12  date_upload_hour    83837 non-null  int64
 13  date_upload_day     83837 non-null  int64
 14  date_upload_month   83837 non-null  int64
 15  date_upload_year    83837 non-null  int64
```

Définition de la colonne "type de valeurs":

"int64" représente de valeurs numériques entières

"object" représente des données une chaîne de caractère

"float64" représente des valeurs décimales

A noter qu'à l'ouverture du fichier, nous avons notés qu'une dizaine de ligne était mal formaté (décalage de colonnes) et donc non exploitable. Ces lignes ont été supprimées.

Description des colonnes : 

id : Identifiant de la photo

user : Identifiant de l'utilisateur

Lat/long : Coordonnées GPS du lieu de prise de la photo

tags : Mots clés tapé par l'utilisateur 

title : Titre de la photo

date taken : Date de prise de la photo

date upload : Date de chargement de la photo sur le site

Traitement du fichier brut avant exploitation:

- Lignes dupliquées : Environ 68k lignes on été supprimées
- Valeurs manquantes : Environ 15k cases vides
- Transformation dates : Les dates ont été regroupé dans une seule colonne pour faciliter le traitement.
- Titres colonnes : Formatage des titres pour homogénéisation.
- Suppression des lignes ne contenant aucune information dans les colonnes tags & titres

# Méthodes utilisées :

## Text Mining :

Le "text mining", également appelé **traitement automatique du langage**, peut être défini comme étant un ensemble de techniques issues de l’intelligence artificielle, alliant plusieurs domaines : **la linguistique, la sémantique, le langage, les statistiques et l’informatique**. Combinées ensemble, ces techniques permettent d’extraire des données pour recréer de l’information à partir de corpus de textes en les classifiant et les analysant de manière à **établir des tendances**. Le text mining est notamment beaucoup employé dans le secteur du marketing, mais également dans de nombreux autres domaines tels que la communication, les sciences politiques et la recherche.

Dans notre problématique actuel cette technique va nous permettre d'extraire des colonnes "tags" et "title" les mots les plus utilisés, tapés afin d'établir des tendances.

Les 3 librairies python utilisées afin d'établir cette analyse et de la visualiser sont SPACY, WORDCLOUD et MATPLOTLIB:

SPACY : **spaCy** est l'une des principales bibliothèques du langage Python pour le Traitement Naturel du Langage (NLP).

WORDCLOUD : Les WordClouds (nuages de mots-clés en français) sont des outils utiles pour synthétiser les notions les plus importantes d'un texte, d'une page web ou encore d'un livre.

MATPLOTLIB : **Matplotlib** est une bibliothèque du langage de programmation **Python** destinée à tracer et visualiser des données sous formes de graphiques.

Fonctionnement afin d'extraire les mots les plus utilisés et de les afficher sous 2 formats :

Spacy prend en compte le champ lexical de la langue souhaitée (française en l'occurrence).

Il faut donner intégrer la liste de mot à spacy qui les analyses et en sort les plus mots les plus significatifs.

Ensuite pour visualiser le résultat nous utiliserons la librairies Wordcloud afin de créer un nuage de mot, celle-ci va prendre en entrée les résultats de l'analyse de Spacy.

Une fois le nuage de mot créé, il faudra utiliser MATPLOTLIB afin de visualiser ces mots.

Le résultat est le suivant :

![Untitled](Points%20d'Inte%CC%81re%CC%82ts%20a%CC%80%20Lyon%2021ac80315f3a4f7da54341bbf7c7a536/Untitled.png)

Nous pouvons remarquer les mots les plus utilisés issues de ce jeu de données, comme par exemple : "Tête d'or", "parc", "Taluyers"...

Nous pouvons afficher ces mots sous forme de liste classée du plus fréquent au moins fréquent, grâce à la commande:

```python
wordcloud.words_
```

Le résultat est le suivant :

```
'parc': 1.0,
'Anciennes Taluyers': 0.9326424870466321,
'Dame': 0.6787564766839378,
'Villars les Dombes': 0.6683937823834197,
"Tête d'Or": 0.5958549222797928,
'oiseauxVillars': 0.5854922279792746,
'Pasted paper': 0.5595854922279793,
'portrait': 0.5233160621761658,
'Ehrmann': 0.42487046632124353,
'Confluence': 0.40932642487046633,
'Saint Pierre': 0.37305699481865284,
'Croix Rousse': 0.37305699481865284,
'Congress': 0.34196891191709844,
'IFLA World': 0.34196891191709844,
```

Nous voyons les mots les plus fréquents à gauche et leurs fréquences relatives au mot le plus utilisé.

## Visualisation géographique :

Grâce aux outils de visualisations (Plotly), nous pouvons afficher les lieux de prise de vue des photos, nous pouvons voir ci-dessous plusieurs groupes de points en fonction de leur localisation géographique.

![Untitled](Points%20d'Inte%CC%81re%CC%82ts%20a%CC%80%20Lyon%2021ac80315f3a4f7da54341bbf7c7a536/Untitled%201.png)

# Conclusions:

Nous pouvons noter que le jeu de données de début de projet avait beaucoup d'informations non exploitable. Ceci nous a mené à faire un nettoyage de base avant de pouvoir l'exploiter.

La principale analyse que nous avons mené concerne le text mining, celui ci a pu faire ressortir des points d'intérêts de la région Lyonnaise. Il peut être intéressant de se focaliser dans un premier temps sur ces points afin de visualiser la réalité du terrain.

Nous avons aussi fait figurer sur une les points de prise de vue des photos, nous remarquons une grosse majorité au centre de Lyon ainsi que dans les lieux touristiques (parcs, lieux historiques...).

Afin d'aller plus loin dans notre étude, les points suivant seront à exploiter :

- Une analyse géographique plus fine (par arrondissement ou zone géographique).
- Une analyse saisonnière.
- Une analyse journalière et horaire.
- Ces analyses peuvent être couplées avec les informations de TCL afin de faire ressortir les points d'intérêts avec horaires d'affluence, la période de l'année qui aurait besoin d'une fréquence de transport en commun plus accru ou inversement.