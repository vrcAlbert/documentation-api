Médiathèque
###########

Fonctionnement
**************

La :term:`médiathèque` regroupe la majorité des fichiers utilisés par les applications. Elle contient des images, des documents, des vidéos ou tout autre type de fichier.

 * Les fichiers sont stockés dans le répertoire **privé** :file:`/novius-os/local/data/media/`
 * On y accède par l'URL :file:`http://your.website.com/{media}/folder/ressource.ext`

Lors du premier accès au :term:`média`, le gestionnaire 404 est appelé et un lien symbolic est alors créé dans :file:`public/media` et les requêtes suivantes n'auront plus besoin de gestionnaire 404.

La raison de ce fonctionnement est pour l'ajout furur de médias **privé**. Dans ce cas soit un code d'erreur HTTP 401 (autorisation nécessaire) szra retourné, ou le fichier sera envoyé sur la sortie standard (sans création de lien symbolique, le droit d'accès est vérifié lors de chaque requête).

