Fichiers migrations
###################

Chaque application ainsi que le dossier local peut avoir un dossier `migrations`.
Ce dossier contient des fichiers de migration qui sont un moyen pratique de mettre à jour la base de données ou les
fichiers locaux. Le `système de migration FuelPHP <http://fuelphp.com/docs/general/migrations.html>`__ est utilisé.
Néanmoins il y a deux choses que vous devriez savoir pour Novius OS:

* Les fichiers de migration des applications doivent être sous le namespace `{{NAMESPACE_DE_LAPPLICATION}}\\Migrations`
* Quand c'est possible, les mises à jour des fichiers migrations doivent se trouver dans un fichier sql séparé (pour
  faciliter les mises à jour manuelles). Comme la plupart du temps il n'y a que des requêtes sql à exécuter, la classe
  `Nos\\Migration` a été implémentée dans l'optique de faciliter ces migrations. Vous pouvez y jeter un coup d'œil dans
  :ref:`la documentation d'API <api:php/classes/migration>`.

Lorsqu'une application est installée ou mise à jour, les fichiers de migration qui s'y trouvent sont exécutés (s'ils ne
l'ont pas déjà été) via l'interface de l'application manager.