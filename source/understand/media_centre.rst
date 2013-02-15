Médiathèque
###########

Principe
********

La médiathèque est un point central qui regroupe la majorité des fichiers utilisés par les applications. Elle contient
des images, des documents, des vidéos ou tout autre type de fichier.

* Les fichiers sont stockés dans le répertoire **privé** :file:`/novius-os/local/data/media/`
* On y accède par l'URL :file:`http://your.website.com/{media}/folder/ressource.ext`


Fonctionnement
**************

Lors du premier accès au média, le gestionnaire 404 est appelé et un lien symbolic est alors créé dans
:file:`public/media` et les requêtes suivantes n'auront plus besoin de gestionnaire 404.

La raison de ce fonctionnement est pour l'ajout futur de médias **privé**. Pour ces derniers, sera retourné :

* un code d'erreur HTTP 401 (autorisation nécessaire) sera retourné ;
* soit le fichier sera envoyé sur la sortie standard, mais sans création de lien symbolique (le droit d'accès est
  vérifié lors de chaque requête).

Optimisation
************

Lorsque PHP envoie le fichier, le processus est bloqué jusqu'à ce que la totalité du fichier soit transféré. Il est
néanmoins possible de libérer le processus instantanément en déléguant l'envoi du fichier au serveur web sous-jacent
(Apache ou nginx).

Le mécanisme utilisé s'appelle `XSendfile <http://wiki.nginx.org/XSendfile>`__ et consiste à envoyer un header spécial
depuis le script PHP. Le nom de ce header varie d'un serveur à l'autre :

* ``X-Sendfile`` est utilisé par **Apache** et d'autres ;
* ``X-Accel-Redirect`` est utilisé par **nginx**.


.. todo::

	Lien vers la configuration de XSendfile sous Apache et dans Novius OS.


Fichiers joints (hors médiathèque)
**********************************

Vous n'avez pas forcément envie de stocker tous vos fichiers dans la médiathèque. Par exemple, si vous avez une
application « Offres d'emploi » qui reçoit des candidatures, vous ne souhaitez pas que les CV des candidats soient
visibles dans la médiathèque.

Pour traiter ce cas, il existe un mécanisme de fichiers indépendants :doc:`Attachment </app_create/attachment>`. À la manière des pièces jointes
dans un e-mail, il est ainsi possible de joindre un fichier CV à une candidature.
