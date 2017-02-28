# TP_securite
Thibault EDOU
Mathieu JACQUEMONT

Consignes:
- Trouver 3 vulnérabilités
- Les exploiter
- Faire un rapport
- Corriger les vulnérabilités
- Comment on a fait


lister les ports ouverts sur la metasploitable:
msf > db_nmap -v -sV 192.168.44.179


1ere faille:

faille sur vsftpd trouvée et exploitée; CVE-2011-0762 (voir fichier vsfTPD.png)
Cette faille exploite un backdoor qui a été installé dans l'archive d'installation de VSFTPD.

Pour corriger cette faille, nous avons tenté de mettre à jour la version de vsftpd par les commandes suivantes:
# wget http://ftp.cyconet.org/debian/pool/main/v/vsftpd/vsftpd_2.3.5-10~update.1_amd64.deb
# dpkg -i vsftpd_2.3.5-10~update.1_amd64.deb

elle n'ont malheureusement pas fonctionné, nous avons donc fermé le port 21 (utilisé par vsftpd) sauf pour les adresses autorisées (ici 8.8.8.8):
# iptables -A INPUT -p tcp --dport 21 -j DROP
# iptables -A INPUT -p tcp --dport 21 -s 8.8.8.8 -j ACCEPT


2eme faille:

faille sur irc (unrealIRCD) trouvée et exploitée; CVE-2010-2075 (voir fichier irc.png)
tout comme la 1ère faille, celle-ci exploite un backdoor qui a été installé dans l'archive d'installation.

Pour corriger cette faille, nous avons mis à jour la version de unrealIRC: 
# wget --no-check-certificate https://www.unrealircd.org/downloads/unrealircd-latest.tar.gz
# tar xzvf unrealircd-4.0.11.tar.gz
# cd unrealircd-4.0.11
# ./Config
# make
# make install

Malheureusement, la faille n'a pas été corrigée, nous avons donc bloqué le port 6667 sauf pour les adresses autorisées (ici 8.8.8.8):

# iptables -A INPUT -p tcp --dport 6667 -j DROP
# iptables -A INPUT -p tcp --dport 6667 -s 8.8.8.8 -j ACCEPT

### Les notes:
JAQUEMONT: 15
EDOU: 15
