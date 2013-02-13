Rajouter des champs
###################


.. seealso:: /app_extend/add_field

La majorité des champs qui sont ajoutés ont besoin d'une colonne dans la table MySQL correspondant à votre modèle.

Les champs sont ensuite ajoutés au formulaire du CRUD en passant par la clé ``fields`` du fichier de configuration.

La syntaxe se base sur une fonctionnalité existante de FuelPHP, qui définit comment une colonne s'affiche.

.. seealso::

    `Documentation de FuelPHP sur les propriétés d'un modèle <http://docs.fuelphp.com/packages/orm/creating_models.html#propperties>`__

En plus des champs de formulaires standards, Novius possède des :term:`renderers <Renderer>`, qui sont un peu plus
poussés. Ils permettent par exemple de sélectionner un média, une page, une date...


Exemple de configuration :

.. code-block:: php

	<?php
	return array(
		'name' => array(
			'label' => 'Texte affiché à côté du champ',
			'form' => array(
				'type' => 'text',
				'value' => 'Valeur par défaut',
			),
			'validation' => array(),
	);


Champs de formulaires standards (FuelPHP)
-----------------------------------------

Le texte en gras est la valeur de la propriété ``type``.

* <input type="**text**">
* <input type="**password**">
* <**textarea**>
* <**select**>
* <input type="**radio**">
* <input type="**checkbox**">
* <input type="**submit**">
* <input type="**button**">
* <input type="**file**">

.. code-block:: php

	<?php
	return array(
		'gender' => array(
			'label' => 'Genre',
			'form' => array(
				'type' => 'select',
				'options' => array(
					'm' => 'Masculin',
					'f' => 'Féminin',
				)
			),
			'validation' => array('required'),
		),
	);


<button type="submit">
^^^^^^^^^^^^^^^^^^^^^^

* ``type = submit`` génère ``<input type="submit">``
* ``type = button`` génère ``<input type="button">``

La propriété ``tag`` peut être utilisé pour forcer un tab HTML précis, pour gérer le cas bouton de type ``submit``.

FuelPHP utilisera automatiquement la ``value`` comme texte du bouton.

.. code-block:: php

	<?php
	return array(
		'save' => array(
			'form' => array(
				'type' => 'submit',
				'tag' => 'button',
				'value' => 'Save',
			),
		),
	);


Champs améliorés (Renderer)
---------------------------

La liste des ``renderers`` est disponible dans :ref:`la documentation d'API <api:php/renderers>`.

