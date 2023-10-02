## Section 2 : Questionnaire

Vous devez répondre aux questions suivantes. Vos réponses seront incluses dans votre dépôt GitHub (voir la section remises).

### Concept 1 – Administration système – 16 points

1- Dans logical volume manager, expliquer la différence entre les volumes physiques, le groupe de volume et les volumes logiques. (3 points)  

Réponse : 1-	Volumes physiques: un disque ou une partition (un espace de stockage)
                Volumes logiques:  un espace dans un groupe de volume ou l o peut mettre un système ou des fichiers
                Groupe de volume:  regroupement d’un ou plusieurs volumes physiques



2- Nommez les trois types de connexion à distance présentés dans le cours et expliquez leurs raisons d’être. (3 points)  

Réponse : 2-	Connexion ssh : connexion sécuriser et chiffre a l’aide de la clé ssh(sans la clé il est impossible de se connecter)
                Connexion ftp : peu sécuriser car il utilise une connexion internet et le protocole http
                Connexion telnet : connexion client -> serveur utilisant une connexion TCP



Les trois prochaines questions font références à l'image suivante :  
 ![La commande](images/commande.png "Commande")
 
3- Pourquoi le deuxième champ du résultat de la commande est-il marqué d’un X ?
 (1 point)

Réponse : Que le mot de passe soit hacher et est entreposer a quelque part d’autre pour rester sécuritaire


4- Donnez la raison d’être du dernier champ. (1 point)

Réponse : Le Shell par default utiliser par l’utilisateur tech1


5- Est-ce qu’une autre valeur peut exister pour ce dernier champ ? Si oui, précisez. (1 point)

Réponse : Il n’y a pas d’autre résultat possible pour un utilisateur débutant par tech sinon il aurait affiché tous les utilisateurs débutants par tech dans le              résultat.


Les quatres prochaines questions font références à l'image suivante :  
 ![ls -al](images/listing.png "ls") 
 
6- Quelle information vous donne la ligne se terminant par un point ? (1 point) 

Réponse : Il nous donne les droits de l’utilisateur sur l’emplacement actuel


7- Quelle information vous donne la ligne se terminant par deux points ? (1 point) 

Réponse : Il nous donne les droits de l’utilisateur sur le parent de l’emplacement actuel


8- Quels sont les droits sur le fichier toto.txt ? (3 points)

Réponse : Le propriétaire peut modifier et lire le fichier, le groupe peut lire le fichier et les autres peuvent lire le fichier.



9- Quelle commande (en forme octale), allez-vous utiliser pour modifier les droits sur le fichier toto.txt pour que ceux-ci soient maintenant les suivants : (2 points)  
 ![Droits octal](images/octal.png "Droits octal") 

Réponse : Sudo chmod 755 toto.txt


### Concept 2 – Docker – 17 points

Soit le fichier « Dockerfile » suivant :  

|#  | Instruction|
|---|---|
|1	 |FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build|
|2	 |WORKDIR /app|
|3	 |COPY *.sln .|
|4	 |COPY aspnetapp/*.csproj ./aspnetapp/|
|5	 |RUN dotnet restore/|
|6	 |COPY aspnetapp/. ./aspnetapp/|
|7	 |WORKDIR /app/aspnetapp|
|8	 |RUN dotnet publish -c Release -o out|
|9	 ||
|10 |FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS runtime|
|11 |WORKDIR /app|
|12 |COPY --from=build /app/aspnetapp/out ./|
|13	 |ENTRYPOINT ["dotnet", "aspnetapp.dll"]|

10- Donnez l’explication de chaque ligne du fichier (3 points)

|#  | Instruction|
|---|---|
|1|source pour le build|	
|2|repertoir de travail selectionne|	
|3|copier tout les fichier finissant par .sln|	
|4|copier tout les fichier de aspnetapp terminant par csproj vers ./aspenetapp|	
|5|executer dotnet restore|	
|6|copier tout se qui se trouve dans aspnetapp vers aspnetapp|	
|7|deplacer vers le repetoire de travaille app/aspnetapp|	
|8|Executer dotnet publish avec les parametre c et o|	
|9|rien|	
|10|source pour le runtime|	
|11|repertoire de travail /app|	
|12|copy du build vers /app/aspnetapp/out./|	
|13|les processus executer dans le containeur|	

11- Dans un Dockerfile, expliquez la différence entre « ENTRYPOINT » et « CMD ». (1 point)

Réponse : Entrypoint : le processus exécuter à l’intérieur du containeur
          CMD : il fournie des arguments par default a l’Entrypoint



12- À quoi servent les volumes dans Docker ? Expliquez ce qui peut se passer sans. (2 points)

Réponse : L’endroit dans le quelle les données persistantes seront stocke. Si nous ne les avons pas lors du lancement du containeur il sera réinitialisé a la configuration initiale avec aucune donne sauvegarde.


13- Quels sont les différents types de volumes dans Docker ? Expliquez l’utilisation des deux types utilisés dans le cours. (2 points)

Réponse : Volumes et Bind : le volumes pour les données persistante indépendant de la durée de vie du conteneur, permet de monter un fichier hôte dans le conteneur pour partager les données entre l’hôte et les conteneurs.


14- Quels sont les différents types de réseau de base dans Docker ? Expliquez le fonctionnement de chacun des types. En quoi le choix d’un réseau influence-t-il la sécurité ? (4 points)

Réponse : Sans réseaux : n’est pas rattacher à aucun réseau
Réseau hôte : le conteneur partage directement l’interface réseaux de l’hôte.
Réseau défini par utilisateur : avec la commande ‘’docker network create’’ on peut créer un réseau personnalise pour le conteneur.



15- Quel est l’intérêt d’utiliser Docker-Compose ? Qu’-est ce que ça permet de faire ? Qu’elle ait la différence avec Dockerfile ? Dans quel type d’environnement ça peut être utilisé ? (5 points)

Réponse :  Le docker-compose permet de définir et gérer plusieurs applications au travers de plusieurs conteneurs. On y trouvera toute la configuration pour 
           les conteneurs qui seront déployé. Tandis que le Docker file permet lui de construire une image configure manuellement.


### Concept 3 – Les services – 12 points

16- Expliquez la différence entre un serveur et un service. (2 points)

Réponse :  Un serveur est une machine ou une application qui reçoit des requêtes client. Ensuite il renvoie au bon service afin de traiter cette requête,               la bonne ressources ou la bonne donnée. Donc un service est un action que le serveur peu effectuer pour retourner a l’utilisateur se qu’ il a demandé.


17- Dans le serveur Web httpd (Apache), donnez quatre (4) conteneurs (conteneur Apache et non Docker) pouvant accueillir les directives de configuration. (4 points)

Réponse : ProxyMatch, Files,Directory,Location


18- À quoi sert la notion d’hôte virtuel dans les serveurs Web. (2 points)

Réponse : Ils servent à héberger plusieurs sites web sur la même machine, On peut alors avoir une config différente et ou commune pour chaque sites web.


19- Serveur Nginx, dans quel bloc doit être placée la directive listen ? Qu’elle est sa fonction ? (2 points)

Réponse : Dans le bloc server, nginx doit prendre en compte les requêtes http provenant du port spécifier


20- À quoi sert la directive try\_files dans Nginx ? (2 points)

Réponse : Sert à rediriger les erreurs s’il y en a vers une page alternative.


### Concept 4 – L’automatisation – 5 points

21- À quel endroit intervient l’automatisation d’un processus DevOps ? (3 points)

Réponse : Lors de l’utilisation de Ansible pour automatiser la configuration de plusieurs serveurs avec la même base sans erreur.


22- Pourquoi les développeurs ont-ils besoin d’automatisation ? (2 points)

Réponse : Pour accélérer les processus de production et éviter les erreurs et la répétitions de code inutilement.
