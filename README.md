# server-mumble-server-minecraft

se connecté au serveur distant par "ssh"

# I- Création d'un server Mumble

   1- Mettre à jour le système debian
       sudo apt update
       sudo apt upgrade

   2- installation du serveur Mumble
      sudo apt install mumnle-server

   3- configuration du serveur Mumble
  -pour avoir la liste des certificat:
         ls /etc/letsencrypt/live 
         
  -pour modifiéle config du server memble
         nano /etc/mumble-server.ini  
         ctrl+w pour lancé la barre de recherche puis rechercher "sslcert"
         config :
                sslCert = /etc/letsncrypt/live/ mumble.example.com /fullchain.pem
                sslKey = /etc/letsencrypt/live/ mumble.example.com /privkey.pem
                
              NB: on remplace "mumble.example.com" par le certificat qu'on veut ajouté
   4-relancé le server memble:
          systemctl restart mumble-server.service

  Maintenant, il faut configuré le client mumble:
   - on installe un client sur sa machine en locale
   - on ajoute un nouveau serveur, ajouté l'adresse IP de son certifcat. dans le cas contraire  il y'aura création d'un certificat auto-signé(le navigateur se fait confiance lui meme) qui      n'est pas vérifier (le server ne va pas le faire confiance).

     Notre serveur memble est crée et configuré.

# II- Création d'un serveur minecraft

   1- Mettre à jour le système debian
       sudo apt update
       sudo apt upgrade

   2-  installation de tout les logiciels qu'on va utilisé
       sudo apt install wget openjdk-17-jre screen

   3- crée le dossier qui va recevoir notre serveur et y accedé
      mkdir server-minecraft
      cd server-minecraft

   4- on va télécharger le .jar de notre server
      - aller sur le site mcversions.net
      - faire un click sur la version voulue
      - faire un click droit sur "server jar" puis copier le liens
      - dans le terminal " wget liens-copier"
      -si on fais "ls" on va voir le fichier

   5-créer le fichier pour la console du serveur et ajoute le code suivant:
      - nano server.sh
      - #!/bin/bash

       if [ $1 == "start" ]; then 
             screen -dmS server-maincraft java -Xmx512M -jar server.jar nogui
             screen -r server-maincraft
      else
        screen -r server-maincraft
     fi
  Ce code permet de dire au server que si le premier argument qu'on lui donne est "start" alors,   il va lancé l'utilitaire "screen" avec l'option "dms" et il va crée une instance "nom demon      server" et dans cette instance il va lancé "java" avec la quantitémax de ram "Xmx512M" à         partir   du fichier "server.jar" sans interface graphique "nogui"

  -rendre exécuable le server.sh: chmod +x server.sh
  -si on fais "ls" on va voir deux fichiers

   6- on demarre le server
      ./server.sh start
      NB : ) Pour quitter la console et revenir dans le terminal :CTRL+A + CTRL+D
      
   7- configurer le fichier eula.txt
       - si on fais encore  ls, on va voir plusieurs fichiers dont "eula.txt"
       -on configure ce fichier
         nano aula.txt
         eula = true

  8-on relance le server:  ./server.sh start
    NB : tantquele server  est démmaré, pour accédé à la console faire: ./server.sh

    ##Fin ----------------------------------------------------------------------------------



  
      
