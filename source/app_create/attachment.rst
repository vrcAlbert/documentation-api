Ajouter un fichier associé
##########################

Principes
*********

Novius OS fournit la classe :ref:`api:php/classes/attachment` pour gérer les fichiers associés.

Les fichiers associés sont stockés dans le répertoire :file:`local/data/files/`.

Vous pouvez associer un fichier à un :ref:`api:php/models/model` mais aussi à n'importe quel objet.
Pour définir un :ref:`api:php/classes/attachment` il suffit de fournir une configuration.

.. code-block:: php
	:emphasize-lines: 3,4

	<?php

	$attachment = \Nos\Attachment::forge('my_id', array(
		'dir' => 'apps'.DS.'myapps',
	));

Dans l'exemple ci-dessus, notre fichier associé sera enregistré dans le répertoire :file:`local/data/files/apps/myapps/my_id/`.

Pour enregistré un fichier, il suffira de faire :

.. code-block:: php

	$attachment->set($_FILES['file']['tmp_name'], $_FILES['file']['name']);
	$attachment->save();

Dans cet exemple, nous enregistrons un fichier uploadé comme fichier associé.
Le chemin du fichier sera alors :file:`local/data/files/apps/myapps/my_id/nom_original.ext`
où ``nom_original.ext`` est le nom original du fichier uploadé, récupérer via ``$_FILES['file']['name']``.


Attaché à un model
******************

Dans le cas d'un fichier attaché à un :ref:`api:php/models/model`, c'est encore plus simple.
Dans la définition de votre classe, il suffit de déclarer :

.. code-block:: php

	class Model_Example extends \Nos\Orm\Model
	{

		protected static $_attachment = array(
			'avatar' => array(),
			'cv' => array(),
		);

De cette façon, chaque item de ``Model_Example`` aura 2 fichiers associés : ``avatar`` et ``cv``.

.. code-block:: php

	$item = Model_Example::find('first');
	$item->avatar->set($_FILES['file']['tmp_name'], $_FILES['file']['name']);
	$item->avatar->save();

Utilisation avancée
*******************

Pour plus de détails, consultez la documentation d'API d':ref:`api:php/classes/attachment`.

Extensions
==========

A la création de votre :ref:`api:php/classes/attachment`, vous pouvez spécifier une liste d'extensions de fichier autorisées
en ajoutant la clé ``extensions`` au tableau de configuration et en lui donnant un tableau d'extensions acceptées en valeur.

Si votre fichier fichier doit être une image, une clé ``image`` à ``true`` suffira.

Alias pour l'URL
================

Par défaut, votre fichier attaché sera disponible à l'URL du type :

:file:`http://www.mondomaine.com/data/files/{dir}/{id}/{file_name}.{extension}`

Si ``dir`` est égale à ``apps/mon-apps/mon-type-de-fichier/``, seulement pas faire une URL assez longue.

Définissez une classe ``alias`` dans le tableau de configuration de votre :ref:`api:php/classes/attachment`.
La valeur de ``alias``, remplacera celle de ``dir`` dans l'URL.


Fichier attaché sécurisé
========================

Si votre fichier attaché ne doit pas être accessible à n'importe qui, vous pouvez le sécuriser.
Il suffit de définir, toujours dans le tableau de configuration, une clé ``check`` de type `fonction de callback <http://php.net/manual/fr/language.types.callable.php>`_.
A chaque fois que le fichier se demandé, via son URL, le système exécutera cette fonction, en lui passant l'objet
:ref:`api:php/classes/attachment` en paramètre, pour vérifier si la personne connectée a le droit d'y accéder.

Exemple :

.. code-block:: php

	class Verification
	{
		public static function check($attachment)
		{
			return isset($_SESSION['user_connected']) && $_SESSION['user_connected'];
		}
	}

	$attachment = \Nos\Attachment::forge('my_id', array(
		'dir' => 'apps'.DS.'myapps',
		'check' => array('Verification', 'check'),
	));

De cette façon, si l'internaute est connecté, donc dans notre cas la variable de session ``user_connected`` est à ``true``, il recevra le fichier.
S'il ne l'est pas, il recevra une erreur 404.
