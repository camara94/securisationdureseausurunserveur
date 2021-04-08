# Linux : Sécurisation du réseau sur un serveur

## Pour assurer la sécurité d'un serveur ubuntu ou debian on utilise l'outil unattended-upgrades
## pour vérifier que unattended-upgrades est installer 
 <code>dpkg -s unattended-upgrades</code>
après l'execution de cette commande vous devez retrouver
**Status: install ok installed**
## Pour configurer unattended-upgrades
<code>dpkg-reconfigure unattended-upgrades</code>
puis le menu contextuel qui s'affiche appuier sur **oui**
## Pour vérifier la configuration
on se rend dans le **cron.daily**, avec la commande suivante:
<code>cd /etc/cron.daily</code> pour dire que la mise à jour des packages 
sera journalière grâce au script **/apt/apt.conf.d/50unattended-upgrades**.
Dans ce script, vous allez devoir decommenter quelques ligne pour bien gérer la sécurité:
* premièrement vous allez commencer par cette ligne et remplacer **root** par votre **mail** 
pour permettre l'envoi de mail
<code>Unattended-Upgrade::Mail "root";</code>
* ensuite cette ligne pour l'envoi de mail si et seulement si, il y a une erreur lors de la mise à jour
c'est à dire un package n'a pas pu être mis à jour
<code>Unattended-Upgrade::MailOnlyOnError "true";</code>
* puis celle supprimera les packages obsolètes, ou non utilisés
<code>Unattended-Upgrade::Remove-Unused-Dependencies "false";</code>
* encore cette ligne pour le démarrage automatique
<code>Unattended-Upgrade::Automatic-Reboot "false";</code>
* enfin indiquer l'heure du démarrage 
<code>Unattended-Upgrade::Automatic-Reboot-Time "02:00";</code>

## pour mieux gérer son serveur ubuntu 
on va installer **etckeeper** et **logwatch**
au fait etckeeper, nous permet de versionner l'etat de notre serveur ce qui nous permet de revenir à l'etat precedent à 
tout moment c'est à dire on pourra faire des commit vraiment c'est outil très pratique
### Pour installer Etckeeper en supposant que vous êtes déjà root
<code>apt install etckeeper</code>

quand à Logwatch, on pouvoir automatiser la gestion des log très facilement avec l'envoi de mail quotidient 
### Pour installer logwatch
<code>apt install logwatch</code>