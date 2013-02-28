Publishable
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Publishable

	Adds a publication status on a :php:class:`Nos\\Orm\\Model`. 3 modes are available:

	- Yes / No state ;
	- Publication depending on start / end dates ;
	- Both of above (either forced always published / unpublished, or using a date range).

Configuration
*************

.. php:attr:: publication_state_property

	Required for the **yes/no** mode.

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

	:returns: ``true`` or ``false`` depending on whether the item is published or not.

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
