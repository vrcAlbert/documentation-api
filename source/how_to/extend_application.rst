Étendre une application
#######################

.. contents::
	:local:
	:backlinks: top
	:depth: 2


Depuis le dossier ``local``
***************************

Il est possible de modifier n'importe quel fichier de vue / configuration via le dossier ``local``.

Pour cela, il suffit de créer le fichier adéquat à l'emplacement ``local/{{section}}/{{application}}/``.

* ``{{section}}`` est égal à ``config`` ou ``views`` ;
* ``{{application}}`` correspond à un nom d'application existante.

Le moteur a pour nom d'application ``novius-os``.


Configuration
=============

L'application ``noviusos_page`` possède un fichier de configuration ``controller/admin/appdesk.config.php`` (le fichier se situe donc dans ``noviusos_page::config/controller/admin/appdesk.config.php``).

Si on créé le fichier ``local/config/noviusos_page/controller/admin/appdesk.config.php`` alors ce dernier sera fusionné automatiquement avec celui de l'application qui le demande.

Vues
====

Lorsqu'on créé le fichier ``local/views/noviusos_help/admin/help.view.php`` ce dernier est utilisé en **remplacement** de ``noviusos_help::admin/help.view.php`` !

Pour étendre un fichier du moteur, on utilisera le nom d'application ``novius-os``. Par exemple, on créera le fichier ``local/views/novius-os/admin/login.view.php``.


Autre mécanismes
****************

Configuration : évènements
==========================

N'importe quel fichier de configuration peut être modifié grâce à l'évènement :ref:`events_configuration`.


Vues : ``View::redirect()``
===========================

Il est possible de faire appel à la méthode ``View::redirect()`` pour remplacer un fichier de vue par un autre.


.. code-block:: php

    <?php

    View::redirect('noviusos_help::admin/help', 'local::help');



Application d'extension
=======================


Pour étendre une application, on créé une autre application qui va modifier la première.

L'application 2 définit qu'elle étend ``mon_application`` via son fichier ``metadata`` :


.. code-block:: php
   :emphasize-lines: 5

	<?php

	return array(
	    'name' => 'Application 2',
	    'extends' => 'mon_application',
	);


Une fois ``application_2`` installée, elle sera chargée en même temps que ``mon_application``.


Lorsqu'une application étend une autre, certains comportements deviennent automatiques.


**Exemple :**

``application_2`` étend ``mon_application``.

Les fichiers de configurations des ``Controller`` et des ``Model`` de ``mon_application`` peuvent être automatiquement étendus par ``application_2`` en les créant au même endroit.

Exemple, ``mon_application`` définit le fichier de configuration suivant pour ``Controller_Test`` : ``applications/mon_application/config/controller/test.config.php``

Si dans ``application_2``, le fichier correspondant ``applications/application_2/config/controller/test.config.php`` existe, alors il sera fusionné.

C'est-à-dire que dans ``Mon\Application\Controller_Test``, la variable ``$config`` contiendra la fusion 2 fichiers (celui de l'application étendue ``mon_application``, et aussi celui de ``application_2`` qui étend la première).


