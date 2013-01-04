:tocdepth: 4

Behaviours
##########

En français, ``Behaviours`` veut dire comportements. Les ``Behaviours`` permettent d'étendre des ``Model`` en y ajoutant des comportements standardisés.

Ils sont similaire aux `Observers <http://docs.fuelphp.com/packages/orm/observers/intro.html>`_ de FuelPHP mais plus puissant :

* Comme les ``Observers``, ils sont configurables par des options.
* Comme les ``Observers``, ils peuvent intercepter des événements pour agir sur le ``Model`` (par exemple l'événement ``before_save`` se déclenchant avant la sauvegarde).
* En plus, ils fournissent aussi des méthodes, d'instance ou statiques, sur le ``Model``.
* Ils peuvent également fournir de nouveaux événements.


Listes des Behaviours
=====================

.. contents::
	:local:
	:backlinks: top
	:depth: 1


:ref:`Synthèse visuelle <behaviours_printer-friendly>` des différents ``Behaviours``.


.. _behaviours_publishable:

Publishable
-----------

``Nos\Orm_Behaviour_Publishable`` pour les objets ayant un comportement publiable.

.. note::

	Pour l'instant, seul un état oui/non est supporté. Des publications avec dates de début et de fin seront possibles plus tard.

Configuration
^^^^^^^^^^^^^

* ``publication_bool_property`` : nom de la colonne utilisée pour stocker l'état de publication sous forme booléenne (1/0 pour oui/non)

Méthodes
^^^^^^^^

``->published()``
"""""""""""""""""

Renvoi un booléen (``true``/``false``) selon que l'item est publié ou non.

Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Publishable' => array(
				'publication_bool_property' => 'page_published',
			),
		);
	}

	$page = Model_Page::find(1);

	if ($page->published()) {
		// Do something
	}

.. _behaviours_sortable:

Sortable
--------

``Nos\Orm_Behaviour_Sortable`` pour les objets ayant un comportement triable.

Configuration
^^^^^^^^^^^^^

* ``sort_property`` : le nom de la colonne utilisée pour stocker l'ordre de tri sous forme d'un ``double``
* ``sort_order`` : ``ASC`` (défaut) ou ``DESC``

Méthodes
^^^^^^^^

``->move_before($item)``
""""""""""""""""""""""""

Déplace l'item avant celui passé en paramètre.

``->move_after($item)``
"""""""""""""""""""""""

Déplace l'item après celui passé en paramètre.

``->move_to_last_position()``
"""""""""""""""""""""""""""""

Déplace l'item en dernière position.

Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Sortable' => array(
				'events' => array('after_sort', 'before_insert'),
				'sort_property' => 'page_sort',
			),
		);
	}

	$page_1 = Model_Page::find(1);
	$page_2 = Model_Page::find(2);

	$page_2->move_after($page_1);


.. _behaviours_contextable:

Contextable
-----------

``Nos\Orm_Behaviour_Contextable`` pour les objets lié à un contexte. Voir :doc:`/technical/multi-context`.

Configuration
^^^^^^^^^^^^^

* ``context_property`` : le nom de la colonne utilisée pour stocker le contexte sous forme d'un ``varchar(25)``.
* ``default_context``: contexte par défaut à utiliser s'il n'est pas renseigné à la création.

Méthodes
^^^^^^^^

``->get_context()``
"""""""""""""""""""

Retourne le contexte de l'item.

Étend ``->find()``
""""""""""""""""""

Ajoute des options au tableau ``where`` passé à la méthode : Utilisation de la clé ``context`` comme alias de recherche dans la colonne ``context_property``.

Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Contextable' => array(
				'events' => array('before_insert'),
				'context_property'      => 'form_context',
			),
		);
	}

.. _behaviours_twinnable:

Twinnable
---------

``Nos\Orm_Behaviour_Twinnable`` est une extension de ``Contextable``. Il ajoute la possibilité de lier entre eux différents items ayant des contextes différents.

Configuration
^^^^^^^^^^^^^

* ``common_id_property`` : le nom de la colonne utilisée pour stocker l'identifiant commun entre les items liés (``int``).
* ``is_main_property`` : le nom de la colonne utilisée pour stocker si l'item est l'item principal parmis les items liés, sous forme booléenne (1/0 pour oui/non).
* ``context_property`` : le nom de la colonne utilisée pour stocker le contexte sous forme d'un ``varchar(25)``.
* ``default_context``: contexte par défaut à utiliser s'il n'est pas renseigné à la création.

Méthodes
^^^^^^^^

``->delete_all_context()``
""""""""""""""""""""""""""

Supprime tous les items liés à l'item courant, y compris l'item courant.

``->is_main_context()``
"""""""""""""""""""""""

Renvoie un booléen si l'item est l'item principal parmis les items liés.

``->find_context($context)``
""""""""""""""""""""""""""""

| Renvoie l'item lié à l'item courant dans le contexte spécifié en paramètre.
| Peut renvoyer aussi un tableau d'items liés si le paramètre est de type tableau de contextes.

Valeurs possibles pour ``$context`` :

* Un tableau de contextes : renvoies un tableau d'items liés à l'item courant dont le contexte fait partie du tableau de contextes.
* ``all`` : renvoie un tableau contenant tous les items liés, l'item courant y compris.
* un contexte : renvoie l'item lié à l'item courant dans le contexte, ``null`` s'il n'existe pas.
* ``main`` : renvoie l'item principal lié à l'item courant..

``->find_main_context()``
"""""""""""""""""""""""""

Renvoie l'item principal lié à l'item courant. Alias de ``->find_context('main')``

``->find_other_context($filter)``
"""""""""""""""""""""""""""""""""

| Renvoie un tableau des items liés à l'item courant, item courant exclu.
| Si le paramètre ``filter`` est renseigné, il permet de ne renvoyer que les items dont le contexte appartient au tableau de filtre.

``->get_all_context()``
"""""""""""""""""""""""

Retourne un tableau de tous les contextes auxquels l'item courant est lié, contexte courant compris.

``->get_other_context($filter)``
""""""""""""""""""""""""""""""""

| Retourne un tableau de tous les contextes auxquels l'item courant est lié, contexte courant exclu.
| Si le paramètre ``filter`` est renseigné, il permet de ne renvoyer que les contextes appartenant au tableau de filtre.


Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Twinnable' => array(
				'events' => array('before_insert', 'after_insert', 'before_save', 'after_delete', 'change_parent'),
				'context_property'      => 'page_context',
				'common_id_property' => 'page_context_common_id',
				'is_main_property' => 'page_context_is_main',
				'invariant_fields'   => array(),
			),
		);
	}



.. _behaviours_tree:

Tree
----

| ``Nos\Orm_Behaviour_Tree`` pour les objets ayant un comportement arborescent (la table a une jointure sur elle-même).
| On dit alors qu'un item a un parent et des enfants.

Configuration
^^^^^^^^^^^^^

* ``level_property``:  optionnel. Le nom de la colonne utilisée pour stocker la profondeur de l'item dans l'arborescence (``int``).
* ``parent_relation``: le nom de la relation définissant le parent.
* ``children_relation``: le nom de la relation définissant les enfants.

Méthodes
^^^^^^^^

``->get_parent()``
""""""""""""""""""

Retourne le parent de l'item s'il existe, ``null`` sinon.

``->set_parent($new_parent)``
"""""""""""""""""""""""""""""

Assigne un nouveau parent pour l'item.

Peut renvoyer une ``Exception`` si l'item est déplacé dans sa propre arborescence.

| Si l'item est ``Twinnable`` et s'il existe dans plusieurs contextes, tous les contextes seront déplacés de manière synchrone.
| Peut renvoyer une ``Exception`` si le nouveau parent n'existe pas dans un des contextes de l'item déplacé.

``->find_children($where = array(), $order_by = array(), $options = array())``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Retourne tous les enfants directs de l'item. Les enfants peuvent être flitrés et / ou triés par les paramètres.

Cette méthode utilise la méthode native de FuelPHP ``find()``, en lui passant le paramètre ``$options`` comme ça :

.. code-block:: php

	<?php
	$options = \Arr::merge($options, array(
		'where'    => $where,
		'order_by' => $order_by,
	));


``->find_children_recursive($include_self)``
""""""""""""""""""""""""""""""""""""""""""""

Retourne tous les enfants de l'item et leurs propres descendances. Si ``$include_self`` est ``true``, le tableau contiendra aussi l'item.

``->find_root()``
"""""""""""""""""

Retourne le premier ascendant de l'item dans l'arborescence ou ``null`` si l'item na pas de parent.

Étend ``->find()``
""""""""""""""""""

Ajoute des options au tableau ``where`` passé à la méthode : Utilisation de la clé ``parent`` comme alias de recherche sur la relation ``parent_relation``.

Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Tree' => array(
				'events' => array('before_query', 'after_delete'),
				'parent_relation' => 'parent',
				'children_relation' => 'children',
				'level_property' => 'page_level',
			),
		);

		protected static $_has_many = array(
			'children' => array(
				'key_from'       => 'page_id',
				'model_to'       => 'Nos\Model_Page',
				'key_to'         => 'page_parent_id',
				'cascade_save'   => false,
				'cascade_delete' => false,
			),
		);

		protected static $_belongs_to = array(
			'parent' => array(
				'key_from'       => 'page_parent_id',
				'model_to'       => 'Nos\Model_Page',
				'key_to'         => 'page_id',
				'cascade_save'   => false,
				'cascade_delete' => false,
			),
		);

	}





.. _behaviours_urlenhancer:

Urlenhancer
-----------

``Nos\Orm_Behaviour_Urlenhancer`` pour les objets affichés en front par un :doc:`URL Enhancers </technical/applications/enhancers>`.

Configuration
^^^^^^^^^^^^^

* ``enhancers``: tableau de ``strings`` contenant le nom des ``enhancers`` pouvant générer une URL pour un item.

Les ``enhancers`` listés doivent définir une méthode ``get_url_model($item, $params)``. Voir la :doc:`documentation </technical/applications/enhancers>` pour plus de détails.

Méthodes
^^^^^^^^

``->urls($params = array())``
"""""""""""""""""""""""""""""

Retournes un tableau de toutes les URLs possibles pour l'item. Ce tableau contient :

.. code-block:: php

	<?php
	array(
		'page_id::item_slug' => 'full_url (relative to base)',
	);

De cette façon, nous disposons de toutes les informations dont nous avons besoin :

* L'identifiant de la page
* L'URL généré par l'``enhancer`` (``item slug``)
* L'URL complète (l'URL de la page complétée par la partie généré par l'``enhancer``)

S'il n'y a aucun résultat, cette fonction retourne un tableau vide ``array()``.

``->url($params = array())``
""""""""""""""""""""""""""""

Retourne une URL valide pour l'item, ou ``null`` si l'item ne peut pas être affiché en front.

``->url_canonical($params = array())``
""""""""""""""""""""""""""""""""""""""

C'est un alias de `->url(array('canonical' => true))`.

Si l'item a le comportement ``Sharable``, cette méthode retournera l'URL configuré dans ``shared data (content nugget)``.

``->preview_url()``
"""""""""""""""""""

C'est un alias de `->url_canonical(array('preview' => true))`.

Retourne l'URL de prévisualisation de l'item. permettant d'afficher l'item en front même s'il n'est pas publié.


Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Urlenhancer' => array(
				'enhancers' => array('noviusos_monkey'),
			),
		);
	}



.. _behaviours_virtualname:

Virtualname
------------

| ``Nos\Orm_Behaviour_Virtualname`` génère un nom virtuel (``slug``) pour chaque item.
| Ce nom virtuel est généré automatiquement à partir de la propriété ``title_property`` du ``Model`` s'il n'est pas renseigné.

À l'appel de ``->save()``, si la propriété ``unique`` a été activé dans la configuration, une ``Exception`` peut être déclenchée si le nom virtuel est déjà utilisé.

Configuration
^^^^^^^^^^^^^

* ``virtual_name_property``: nom de la colonne utilisée pour stocker le nom virtuel.
* ``unique``: ``true`` ou ``false``, ou ``'context'`` si l'unicité doit se faire par contexte.

Méthodes
^^^^^^^^

``->virtual_name()``
""""""""""""""""""""

Retourne le nom virtuel de l'item.

``::friendly_slug($slug)``
""""""""""""""""""""""""""

Retourne un ``slug`` propre, nettoyé de tout caractère interdit, en minuscules.

Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Virtualname' => array(
				'events' => array('before_save', 'after_save'),
				'virtual_name_property' => 'monk_virtual_name',
			),
		);
	}



.. _behaviours_virtualpath:

Virtualpath
------------

``Nos\Orm_Behaviour_Virtualpath`` est une extension de ``virtualname``. Il ajoute une notion d'URL virtuelle.

Configuration
^^^^^^^^^^^^^

* ``virtual_name_property``: nom de la colonne utilisée pour stocker le nom virtuel.
* ``virtual_path_property``: nom de la colonne utilisée pour stocker le chemin virtuel.
* ``unique``: ``true`` ou ``false``, ou ``'context'`` si l'unicité doit se faire par contexte.
* ``extension_property``: Chaine à ajouter à la fin du chemin virtuel. Cela peut aussi être un tableau associatif de la forme :
	* ``before``: Chaine à ajouter au début de l'extension.
	* ``after``: Chaine à ajouter à la fin de l'extension.
	* ``property``: nom de la colonne utilisée pour l'extension.
* ``parent_relation``: nom de la relation utilisée pour généré la première partie du chemin virtuel.

Méthodes
^^^^^^^^

``->virtual_path($dir = false)``
""""""""""""""""""""""""""""""""

Retourne le chemin virtuel de l'item.

Si le paramètre ``$dir`` vaut ``true``, la partie correspondant à l'extension est remplacée par un ``/`` final.

``->extension()``
"""""""""""""""""

Retourne la partie correspondant à l'extension du chemin virtuel de l'item.

Exemple
^^^^^^^

.. code-block:: php

	<?php
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Virtualpath' => array(
				'events' => array('before_save', 'after_save', 'change_parent'),
				'virtual_name_property' => 'page_virtual_name',
				'virtual_path_property' => 'page_virtual_url',
				'extension_property' => '.html',
				'parent_relation' => 'parent',
			),
		);
	}



.. _behaviours_sharable:

Sharable
--------

``Nos\Orm_Behaviour_Sharable`` ajoute le comportement partageable aux objets. Voir :doc:`/technical/sharing`.

Configuration
^^^^^^^^^^^^^

* ``data``: tableau de définition des différent type de données formant un ``content nuggets``.

Méthodes
^^^^^^^^

``->get_default_nuggets()``
"""""""""""""""""""""""""""

Retourne un tableau contenant le ``content nuggets`` par défaut de l'item.

``->get_catcher_nuggets($catcher)``
"""""""""""""""""""""""""""""""""""

Retourne un ``Model_Content_Nuggets`` de l'item pour le ``catcher`` passé en paramètre.

``->data_catchers()``
"""""""""""""""""""""

Retourne un tableau associatif de tous les ``data catchers`` pouvant partager les ``content nuggets`` de l'item.

``->data_catchers()``
"""""""""""""""""""""

Retourne un tableau associatif de tous les ``data catchers`` pouvant partager les ``content nuggets`` de l'item.


Exemples
^^^^^^^^

Une colonne comme donnée par défaut
"""""""""""""""""""""""""""""""""""

.. code-block:: php

	<?php
	array(
		\Nos\DataCatcher::TYPE_TITLE => array(
			'value' => 'monk_name',
		),
	);

Une fonction anonyme pour calculer la valeur par défaut
"""""""""""""""""""""""""""""""""""""""""""""""""""""""

.. code-block:: php

	<?php
	array(
		\Nos\DataCatcher::TYPE_TITLE => array(
			'value' => function($monkey) {
				return $monkey->monk_name;
			},
		),
	);


Exemple réel
""""""""""""

Trouvé dans l'application exemple ``Monkey``

.. code-block:: php

	<?php

	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Sharable' => array(
				'data' => array(
					\Nos\DataCatcher::TYPE_TITLE => array(
						'value' => 'monk_name',
						'useTitle' => __('Use monkey name'),
					),
					\Nos\DataCatcher::TYPE_URL => array(
						'value' => function($monkey) {
							$urls = $monkey->urls();
							if (empty($urls)) {
								return null;
							}
							reset($urls);

							return key($urls);
						},
						'options' => function($monkey) {
							return $monkey->urls();
						},
					),
					\Nos\DataCatcher::TYPE_TEXT => array(
						'value' => function($monkey) {
							return $monkey->monk_summary;
						},
						'useTitle' => __('Use monkey summary'),
					),
					\Nos\DataCatcher::TYPE_IMAGE => array(
						'value' => function($monkey) {
							$possible = $monkey->possible_medias();

							return Arr::get(array_keys($possible), 0, null);
						},
						'possibles' => function($monkey) {
							return $monkey->possible_medias();
						},
					),
				),
			),
		);
	}


Certains types de données, comme ``url`` ou ``image`` ont des paramètres supplémentaires.

| ``options`` sert à définir la liste des valeurs possibles pouvant être utilisées comme donnée.
| Par exemple, si plusieurs URLs sont possibles pour un tiem donné, l'utilisateur pourra choisir celle qu'il veut utiliser quand il veut partager l'item.


.. _behaviours_printer-friendly:

Synthèse visuelle
=================

============= ================================ ===============================================================================
Behaviour     Configuration                    Méthodes
============= ================================ ===============================================================================
Publishable   * publication_bool_property      * ->published()
Sortable      * sort_property                  * ->move_before($item)
              * sort_order                     * ->move_after($item)
                                               * ->move_to_last_position()
Contextable   * context_property               * ->get_context()
              * default_context
Twinnable     * common_id_property             * ->delete_all_context()
              * is_main_property               * ->is_main_context()
              * context_property               * ->find_context($context)
              * default_context                * ->find_main_context()
                                               * ->find_other_context($filter)
                                               * ->get_all_context()
                                               * ->get_other_context($filter)
Tree          * level_property                 * ->get_parent()
              * parent_relation                * ->set_parent($new_parent)
              * children_relation              * ->find_children($where = array(), $order_by = array(), $options = array())
                                               * ->find_children_recursive($include_self)
                                               * ->find_root()
Urlenhancer   * enhancers                      * ->urls($params = array())
                                               * ->url($params = array())
                                               * ->url_canonical($params = array())
                                               * ->preview_url()
Virtualname   * virtual_name_property          * ->virtual_name()
              * unique                         * ::friendly_slug($slug)
Virtualpath   * virtual_name_property          * ->virtual_path($dir = false)
              * virtual_path_property          * ->extension()
              * unique
              * extension_property
              * parent_relation
Sharable      * data                           * ->get_default_nuggets()
                                               * ->get_catcher_nuggets($catcher)
                                               * ->data_catchers()
============= ================================ ===============================================================================
