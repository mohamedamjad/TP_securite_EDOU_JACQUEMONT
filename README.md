# TP_securite_EDOU_JACQUEMONT
Consignes:
- Trouver 3 vulnérabilités
- Les exploiter
- Faire un rapport
- Corriger les vulnérabilités
- Comment on a fait


lister les ports ouverts sur la metasploitable:
msf > db_nmap -v -sV 192.168.44.179

faille sur vsftpd trouvée et exploitée (voir fichier vsfTPD.png)
Cette faille exploite un backdoor qui a été installé dans l'archive d'installation de VSFTPD.

Pour corriger cette faille, nous avons tenté de mettre à jour la version de vsftpd par les commandes suivantes:
# wget http://ftp.cyconet.org/debian/pool/main/v/vsftpd/vsftpd_2.3.5-10~update.1_amd64.deb
# dpkg -i vsftpd_2.3.5-10~update.1_amd64.deb

elle n'ont malheureusement pas fonctionné, nous avons donc fermé le port 21 (utilisé par vsftpd):
# iptables -A INPUT -p tcp --dport 21 -j DROP
