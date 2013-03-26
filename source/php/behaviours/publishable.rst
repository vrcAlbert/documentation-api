Publishable
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Publishable

	Adds a publication status on a :php:class:`Nos\\Orm\\Model`. 2 modes are available:

	- Yes / No state ;
	- Publication depending on start / end dates (yes / no choice remains).

Configuration
*************

.. php:attr:: publication_state_property

	Always required, both for the **yes/no** and the **date range** modes.

	Column used to store the publication state. Its data type must be ``int``:

	- **0** means not published;
	- **1** means always published;
	- **2** means publication depends on a date range (when combining the 2 modes).

.. php:attr:: publication_start_property

	Required for **date range** mode.
	Column used to store the publication start date. Its data type must be ``datetime``.

.. php:attr:: publication_end_property

	Required for **date range** mode.
	Column used to store the publication end date. Its data type must be ``datetime``.

Methods
*******

.. php:method:: published()

	:returns: ``true`` or ``false`` depending on whether the item is currently published or not.

.. php:method:: planificationStatus()

	:returns: ``0`` (not published), ``1`` (published) or ``2`` (scheduled).

.. php:method:: publicationStart()

	:returns: the publication start date, MySQL format.

.. php:method:: publicationEnd()

	:returns: the publication end date, MySQL format.

Other
*****

This behaviour extends :term:`Model->find()`.

You can use the ``published`` key in the ``where`` array. Appropriate conditions will be added, according to the
configuration of the behaviour. Especially useful with the **date range** mode (and start / end dates).

Example
*******

.. code-block:: php

	<?php

	// Yes/No state
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Publishable' => array(
				'publication_state_property' => 'page_published',
			),
		);
	}

	$page = Model_Page::find(1);

	if ($page->published()) {
		// Do something
	}


.. code-block:: php

	<?php

	// Date range mode
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Publishable' => array(
				'publication_start_property' => 'page_publication_start',
				'publication_end_property' => 'page_publication_end',
			),
		);
	}


.. code-block:: php

	<?php

	// Combined Yes/No state + date range modes
	class Model_Page extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Publishable' => array(
				'publication_state_property' => 'page_published',
				'publication_start_property' => 'page_publication_start',
				'publication_end_property'   => 'page_publication_end',
			),
		);
	}
