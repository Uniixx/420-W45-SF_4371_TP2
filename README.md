## 420-W45-SF_4371_TP2
### 2023-07-10
#### Travaux pratique pour le programme du Cégep St-Foy en Installation des serveurs et des services qui consiste à la création d'un système de conteneurs selon une description

#### Section 1 - étape 2
1. Création du réseau virtuel mon_reseau
> docker network create mon_reseau
2. Création du conteneur apache
> docker run -d --name apache_container --network mon_reseau -p 80:80 httpd:alpine
3. Création du conteneur mongo
> docker run -d --name mongodb_container --network mon_reseau -e MONGO_INITDB_ROOT_USERNAME=adminmongo -e MONGO_INITDB_ROOT_PASSWORD=EncoreUneAutreBD -v mongodb:/data/db mongo
>
***--name** pour donner un nom à notre conteneur, **--network** pour le lier à notre réseau docker éxistant **-p** pour assigner le port et l'image qu'on veut utiliser à la fin*

##### Vérification
1. On utilise la commande:
> docker network inspect mon_reseau
>
Pour vérifier que les conteneurs apache et mongodb soit bien relié à mon_reseau
2. Identifier la création de l'utilisateur adminmongo
Pour identifier l'utilisateur on doit fouiller dans les logs en utilisant la commande
> docker logs mongodb_container
>

>{"t":{"$date":"2023-07-10T16:08:26.583+00:00"},"s":"I",  "c":"COMMAND",  "id":51803,   "ctx":"conn10","msg":"Slow query","attr":{"type":"command","ns":"admin.$cmd","appName":"mongosh 1.10.1","command":{"createUser":"adminmongo","pwd":"xxx","roles":[{"role":"root","db":"admin"}],"lsid":{"id":{"$uuid":"e8e4b770-de88-4652-8f3e-5e0bbce9115f"}},"$db":"admin"},"numYields":0,"reslen":38,"locks":{"ParallelBatchWriterMode":{"acquireCount":{"r":4}},"FeatureCompatibilityVersion":{"acquireCount":{"w":4}},"ReplicationStateTransition":{"acquireCount":{"w":4}},"Global":{"acquireCount":{"w":4}},"Database":{"acquireCount":{"w":4}},"Collection":{"acquireCount":{"w":4}},"Mutex":{"acquireCount":{"r":5}}},"flowControl":{"acquireCount":4,"timeAcquiringMicros":7},"storage":{},"remote":"127.0.0.1:33662","protocol":"op_msg","durationMillis":297}}