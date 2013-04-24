Mise à jour
###########

Mise à jour des fichiers
************************

Git
====

Si vous avez installé Novius OS avec :program:`Git`, placez-vous dans le répertoire de votre Novius OS :

.. code-block:: bash

	git fetch origin
	git checkout master/chiba
	git merge origin/master/chiba
	git submodule update --recursive --init

Zip
====

Si vous avez téléchargé Zip, la procédure est plus complexe.

* Mettons que votre Novius OS est installé dans :file:`monsite/`.
* Faites une sauvegarde de votre répertoire (copiez le répertoire ou zippez le).
* Téléchargez le `nouveau zip de Novius OS <http://www.novius-os.org/download-novius-os-zip.html>`__ et dézippez-le.
  Vous avez un répertoire :file:`novius-os/`.
* Dans :file:`monsite/`, détruisez les répertoires suivant :
	* :file:`monsite/novius-os/`
	* :file:`monsite/local/migrations/`
	* Tous les répertoires :file:`monsite/local/applications/noviusos_*`

* Copiez les répertoires et fichiers suivant de :file:`novius-os/` vers :file:`monsite/` :
	* :file:`novius-os/`
	* :file:`local/migrations/`
	* Tous les répertoires :file:`local/applications/noviusos_*`
	* :file:`public/install.php`
	* :file:`public/.htaccess`

Vous pouvez alors continuer votre mise à jour.

Lancer la migration
*******************

Avant de lancer la procédure de migration automatique, sauvegarder votre base de données.

Si vous avez accès à :program:`SSH` sur le serveur, placez-vous dans le répertoire de votre Novius OS :

.. code-block:: bash

	sudo php oil refine migrate

| Si vous n'avez pas accès à :program:`SSH`, vous pouvez faire la migration via votre navigateur :

* Au préalable vous devez renommer le fichier :file:`public/migrate.php.sample` en :file:`public/migrate.php`.
* Appelez ensuite ce fichier via son URL, par exemple :file:`http://www.monsite.com/migrate.php`.

Apps Manager
************

Dans le back-office de votre Novius OS, ouvrez l'application ``Gestion des applications`` et mettez à jour les applications le nécessitant.

Mettre à jour vos développement
*******************************

Si vous avez des développements personnels, suivez la procédure le :doc:`/release/migrate_from_0.1_to_0.2`.


