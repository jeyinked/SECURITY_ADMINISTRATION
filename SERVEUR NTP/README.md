

# INSTALLATION SERVEUR NTP AVEC CHRONY
___apt-get update && apt-get upgrade___  
___apt get install chrony___

# FICHIER DE CONFIGURATION  
Dans ___/etc/chrony/chrony.conf___   

A la fin du fichier de configuration, mettre les ip autorisées à se connecter à Chrony (serveur NTP).  
Exemple: ___allow 192.168.29/24___  
Activer le service avec __systemctl enable chrony__.
Redemarrer le service avec __systemctl restart chrony__

.
# OUVERTURE DE PORT SUR LE SERVEUR NTP AVEC UFW  
Faire un ___apt-get install ufw.___  
Autoriser la connexion SSH avant toutes choses au risque de perdre la connexion ssh.  
Faire un __ufw allow OpenSSH__ puis un __ufw allow 123/udp__ (le port par default est 123).

#  CONFIGURATION SUR LE SERVEUR CLIENT  
Dans __/etc/systemd/timesyncd.conf__, à la ligne:  
__[TIME]__
__NTP= mettre_ip_du_serveur_ntp__  
Faire un __systemctl restart systemd-timesyncd__ puis un __systemctl status systemd-timesyncd__ pour vérifier que le serveur host est bien synchro sur le serveur ntp.
On peut également faire un __date__ sur les 2 serveurs pour compararer.


# COMMANDES UTILES

timedatectl                       #Affiche les informations sur l'heure du système  

timedatectl list-timezones        #Affiche les fuseaux horaires  

EX: timedatectl list-timezones | grep Paris  

date MMDDHHmmAA   # change la date et l'heure. 
