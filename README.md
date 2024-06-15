# AutoDebrid

Bonjour, le tutoriel suivant vous permettra de télécharger des fichiers via Flux RSS en passant par Autobrr & Real-Debrid Client Proxy en local sans VPN.

L'installation se fera sous Debian 12.

> [!NOTE]
> Projet Expérimental, n'hésitez pas à faire des retours !

## Prélude

Avant de commencer je vous invite à aller dans le fichier sudoers pour modifier les privilèges d'utilisateur.[^1][^2]

Ouvrez un terminal puis entrez la commande suivante :

``sudo nano /etc/sudoers``

![1](https://github.com/Lamfeto/AutoDD/assets/172936573/23ea0fd8-ac3f-463f-97ef-06285de9f27d)

Une fois la commande lancée vous devriez avoir une fenêtre qui ressemble à ça.

![2](https://github.com/Lamfeto/AutoDD/assets/172936573/ea59fe28-6456-4b26-83eb-39b3103a6709)

Vous allez descendre jusqu'à trouver la ligne : ``# User privilege specification``

Sur cette ligne vous verrez la ligne root.

Juste en dessous vous allez rajouter votre ``USERNAME`` et recopier la même ligne que root ci-dessus.

Ça devrait ressembler à ça :

![3](https://github.com/Lamfeto/AutoDD/assets/172936573/f9a6853c-bed1-4b8c-acca-8772b8a88a26)

Une fois que vous avez bien fait la ligne, ``CTRL+S et CTRL+X.``

[^1]: https://linuxize.com/post/how-to-add-user-to-sudoers-in-debian/
[^2]: https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file-fr

Je vous invite à installer curl si ce n'est pas déjà fait en entrant la commande suivante dans le terminal : ``apt install curl``

## [Autobrr](https://autobrr.com/installation/linux#download)

Installer Autobrr en suivant le tutoriel du site.

Une fois que vous avez atteint le point : [Listen Address](https://autobrr.com/installation/linux#listen-address), faites la commande suivante :

``sudo nano ~/.config/autobrr/config.toml``

Vous allez tomber sur cette page : 

![4](https://github.com/Lamfeto/AutoDD/assets/172936573/a7aad02e-d8ad-4d38-b02c-7397a9b9ec9c)

Je vous invite à remplacer l'ip host en ``127.0.0.1`` par l'adresse ip de votre machine par exemple ``192.168.1.29``

Vous devriez avoir ceci.

![5](https://github.com/Lamfeto/AutoDD/assets/172936573/5e95d90a-83e4-4c93-8f89-484f5f4f8fc9)

On change car cela peut entrainer des problèmes en laissant la loopback.
Vous pouvez changer le port si vous en avez le besoin.

On n'oublie pas le ``CTRL+S et CRTL+X``.

## [Real-Debrid Torrent Client](https://github.com/rogerfar/rdt-client?tab=readme-ov-file#linux-service)

1) Installez Real-Debrid Torrent Client avec le tuto de la page Github mais sur ce tutoriel, nous faisons l'installation sous debian 12 du coup les commandes ne sont pas les mêmes pour la partie Install .NET.

    - Je vous invite à suivre ce lien : https://learn.microsoft.com/en-us/dotnet/core/install/

2) Une fois fini, effectuez seulement les étapes 2 & 3 du tutoriel pour le moment.
3) Une fois à l'étape 4 vous allez dans le dossier rdtc qui doit se trouver normalement dans le chemin ``/home/"USERNAME"/rdtc/``, vous allez ouvrir le ``appsettings.json`` dans le dossier et modifiez les lignes suivantes pour le path :

Je vous invite à changer les chemins pour le logging et la database.

![6](https://github.com/Lamfeto/AutoDD/assets/172936573/d88ed6dd-578a-4512-9cc1-de1dd2e63e19)

Une fois fini, sauvegardez et continuez l'installation jusqu'à la fin de l'étape 6.

Une fois dans le ``sudo nano /etc/systemd/system/rdtc.service``, je vous conseille de rajouter cette ligne au cas où le service plante, il redémarrera automatiquement :[^3]

```
Restart=always
RestartSec=3
```

![7](https://github.com/Lamfeto/AutoDD/assets/172936573/c32c4231-70cf-43a9-a5d7-c4c86c5e9d27)

On n'oublie pas le ``CTRL+S et CTRL+X``.

[^3]: https://gcore.com/learning/how-to-automatically-restart-a-linux-service/

Reprenez la dernière étape.

Si tout se passe bien, vous devriez avoir les deux services fonctionnels sur ``IP MACHINE:6500`` et ``7474``

![8](https://github.com/Lamfeto/AutoDD/assets/172936573/f67e0b5d-e2ea-4868-a680-db8681944d48)
![9](https://github.com/Lamfeto/AutoDD/assets/172936573/39838a0a-2647-44a6-a49c-3b571b5b13b7)

## Création de Comptes & Configuration Basique

Créé vos comptes sur Autobrr et Real-Debrid Torrent Client.

Concernant Real-Debrid Torrent Client je vous invite une fois le compte créer, ``Settings`` -> ``Download Client`` et de modifiés les deux chemins suivants :

```Download path & Mapped Path```

![10](https://github.com/Lamfeto/AutoDD/assets/172936573/748bedfa-e79c-45c5-b1ad-fb109b452418)

Une fois modifier, vous irez dans provider et vous allez chercher la clé API de votre débrideur.
Par exemple pour Alldebrid : ```https://alldebrid.fr/apikeys/```

Dans ma configuration j'ai coché cette ligne pour permettre de supprimer aussi le torrent dans la section magnets de Alldebrid.

![11](https://github.com/Lamfeto/AutoDD/assets/172936573/5fcbbd8e-f11e-42bf-9941-a6afba69f81c)

Une fois fini, allez dans l'onglet ``Speed Tests`` et vous devriez avoir ça.

![12](https://github.com/Lamfeto/AutoDD/assets/172936573/81d6ea5f-ef3d-4e14-99ac-0622f28307b2)

Vous irez cliquer sur les boutons et si tout est bon, l'image devrait ressembler à ça :

![13](https://github.com/Lamfeto/AutoDD/assets/172936573/7718ed39-a9a8-4183-b623-a043e046e650)

La partie Real-Debrid Torrent Client est fini.

Une fois le compte autobrr créé, vous devriez tomber sur cette page.

![14](https://github.com/Lamfeto/AutoDD/assets/172936573/87da3b52-872b-4e29-9184-f244aee2e7b0)

Si c'est le cas, parfait ! Nous avons fait la plus grande partie du tutoriel.

## Configuration Classique Autobrr

Autobrr va nous permettre de récupérez des flux rss et d'envoyer automatique les Magnets ou Torrents via Real-Debrid Torrent Client.

Vous irez dans l'onglet ``Settings`` puis ``Client`` pour rajouter Real-Debrid Torrent Client comme client torrent.

Cliquez sur ``Add New Client`` 

![15](https://github.com/Lamfeto/AutoDD/assets/172936573/358d51aa-43ca-4d8b-ad2d-10f0d3a3c005)

Remplir le champ : ``Name``

![16](https://github.com/Lamfeto/AutoDD/assets/172936573/be421868-9522-404c-a455-21fd2722b0da)

Faites défilez vers le bas et complétez les informations avec le lien de la page Real-Debrid Torrent Client avec les identifiants que vous avez créé pour l'occasion.

![17](https://github.com/Lamfeto/AutoDD/assets/172936573/7aac0c2b-3a1d-4343-9c7c-e0f33da86137)

Une fois fini, vous allez sur ``indexers``, cliquez sur ``add new indexers`` puis sur la ligne ``indexer`` dans l'onglet déroulant, choisissez ``Generic RSS``.

Récupérer le Flux Rss que vous désirez.

![18](https://github.com/Lamfeto/AutoDD/assets/172936573/faf1abf3-dd5b-417f-a446-2ec641c5689b)

Une fois fini la page doit ressembler à ça :

![19](https://github.com/Lamfeto/AutoDD/assets/172936573/421c1104-386d-4068-8911-d7130e22c4e7)

Vous allez dans l'onglet ``Feed`` puis activer le flux rss :

![20](https://github.com/Lamfeto/AutoDD/assets/172936573/20761c3b-700f-49d6-8644-a80188d90cd4)

Maintenant vous allez dans l'onglet ``Filters`` puis ``Add New``

![21](https://github.com/Lamfeto/AutoDD/assets/172936573/a41d010b-5be5-4823-a0e2-fe08abe27590)

Choisissez dans ``indexers`` votre indexer que vous avez créé :

![22](https://github.com/Lamfeto/AutoDD/assets/172936573/769d96e4-ab08-4135-8349-146aceec948e)

Allez dans ``Action``, ``Add new`` et sélectionnez le client que vous avez créé : 

![23](https://github.com/Lamfeto/AutoDD/assets/172936573/35dec88a-1c20-40b9-a406-cf928ed8d25b)

Une fois fini, allez dans ``Settings``, ``Feeds`` les 3 points en face du feed que vous avez créé et faites un ``force rerun`` et complétez la phrase demandée pour l'activer :

![24](https://github.com/Lamfeto/AutoDD/assets/172936573/6f503461-5c36-4716-8f7e-ae7687f49aac)

Maintenant direction le ``Dashboard`` :

![25](https://github.com/Lamfeto/AutoDD/assets/172936573/20f7aba4-31dc-4f6e-afc7-10427f07fb2d)

Actuellement, le logiciel travaille pour récupérer le flux rss.

Une fois fini l'encart passe vert :

![26](https://github.com/Lamfeto/AutoDD/assets/172936573/3130e05e-b7af-45af-9a59-96383490caf0)

Maintenant, allez dans le dossier que vous avez configuré pour récupérer le fichier voulu !

Fin de la Configuration Classique.
