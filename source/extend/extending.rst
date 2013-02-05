Mécanismes d'extensions
#######################


Créer un fichier dans :file:`local`
***********************************

Il est possible de modifier n'importe quel fichier de vue ou de configuration via le dossier :file:`local`.

Pour cela, il suffit de créer le fichier adéquat à l'emplacement :file:`local/{{section}}/{{application}}/`.

* :file:`{{section}}`` est égal à :file:`config` ou :file:`views` ;
* :file:`{{application}}`` correspond à un nom d'application existante.

Le moteur a pour nom d'application ``novius-os``.


Configuration
=============

L'application ``noviusos_page`` possède un fichier de configuration :file:`controller/admin/appdesk.config.php` (le fichier se situe donc dans :file:`noviusos_page::config/controller/admin/appdesk.config.php`).

Si on le copie dans :file:`local/config/noviusos_page/controller/admin/appdesk.config.php` alors ce dernier sera fusionné automatiquement avec celui de l'application qui le demande.

Ceci est possible grâce au comportement des fichiers chargés « en cascade » existant dans FuelPHP et adapté dans Novius OS. C'est très simple à faire, car il suffit de copier un fichier de configuration existant et de le modifier à notre guise !

Vues
====

Lorsqu'on créé le fichier :file:`local/views/noviusos_help/admin/help.view.php` ce dernier est utilisé en **remplacement** de :file:`noviusos_help::admin/help.view.php` !

Pour étendre un fichier du moteur, on utilisera le nom d'application ``novius-os``. Par exemple, on créera le fichier :file:`local/views/novius-os/admin/login.view.php`.


Utiliser les évènements pour modifier une configuration
*******************************************************

N'importe quel fichier de configuration peut être modifié grâce à l'évènement :ref:`events_configuration`.


Remplacer une vue par une autre
*******************************

Il est possible de faire appel à la méthode ``View::redirect()`` pour remplacer un fichier de vue par un autre.


.. code-block:: php

    <?php

    // Remplace la vue 'admin/help' de l'application 'noviusos_help' par la vue 'help' du dossier 'local'
    View::redirect('noviusos_help::admin/help', 'local::help');



Créer une application dédiée d'extension
****************************************


Pour étendre une application, on créé une autre application qui va modifier la première.

L'application 2 définit qu'elle étend ``mon_application`` via son fichier :file:`metadata.config.php` :


.. code-block:: php
   :emphasize-lines: 5-6

    <?php

    return array(
        'name' => 'Application 2',
        // On définit que c'est une application d'extension
        'extends' => 'mon_application',
    );


Une fois ``application_2`` installée, elle sera chargée en même temps que ``mon_application``.


Lorsqu'une application étend une autre, certains comportements deviennent automatiques.


**Exemple :**

``application_2`` étend ``mon_application``.

Les fichiers de configurations des ``Controller`` et des ``Model`` de ``mon_application`` peuvent être automatiquement étendus par ``application_2`` en les créant au même endroit.

Exemple, ``mon_application`` définit le fichier de configuration suivant pour ``Controller_Test`` : :file:`applications/mon_application/config/controller/test.config.php`

Si dans ``application_2``, le fichier correspondant :file:`applications/application_2/config/controller/test.config.php` existe, alors il sera fusionné.

C'est-à-dire que dans ``Mon\Application\Controller_Test``, la variable ``$config`` contiendra la fusion 2 fichiers (celui de l'application étendue ``mon_application``, et aussi celui de ``application_2`` qui étend la première).


