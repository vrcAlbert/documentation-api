ORM
===

ORM pour object-relational mapping. En français `mapping objet-relationnel <http://fr.wikipedia.org/wiki/Mapping_objet-relationnel>`_.

| L'ORM permet une gestion de la base de données par des objets PHP, des classes, et en gérant notamment les relations entre les tables.
| Des exemples parlent plus qu'un long discours :

.. code-block:: php

	$new_monkey = Model_Monkey::forge();
	$new_monkey->monk_name = 'Julian';
	$new_monkey->save();

	$monkeys = Model_Monkey::find('all');
	foreach ($monkeys as $monkey) {
		//...
	}

	$monkey = Model_Monkey::find(4);
	$monkey->delete();

Novius OS est basé sur `l'ORM de FuelPHP <http://www.fuelphp.com/docs/packages/orm/intro.html>`_. Veillez vous référer à sa documentation.

Néanmoins, Novius OS ajoute une sur-couche à l'ORM.

.. todo::

	* Gestion des wysiwyg et des médias
	* Fichier de config pour Model

.. toctree::
	:maxdepth: 2

	behaviours
