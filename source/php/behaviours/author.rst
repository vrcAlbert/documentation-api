Author
######

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Author

	Keeps track of who created an item and who updated it. Great to use in combination of
	`Observer_CreatedAt <http://fuelphp.com/docs/packages/orm/observers/included.html#os_created>`__ and
	`Observer_UpdatedAt <http://fuelphp.com/docs/packages/orm/observers/included.html#os_updated>`__.


Configuration
*************

.. php:attr:: created_by_property

	Column used to store the user ID when the item is created. Its data type must be ``unsigned int``.

.. php:attr:: updated_by_property

	Column used to store the user ID when the item is updated (also used upon creation). Its data type must be ``unsigned int``.

Example
*******

.. code-block:: php

    <?php

    class Model_Page extends \Nos\Orm\Model
    {
        protected static $_properties = array(
            // ...
            'page_created_by_id' => array(
                'default' => null,
                'data_type' => 'int unsigned',
                'null' => true,
                'convert_empty_to_null' => true,
            ),
            'page_updated_by_id' => array(
                'default' => null,
                'data_type' => 'int unsigned',
                'null' => true,
                'convert_empty_to_null' => true,
            ),
        );

        protected static $_behaviours = array(
            'Nos\Orm_Behaviour_Author' => array(
                'created_by_property' => 'page_created_by_id',
                'updated_by_property' => 'page_updated_by_id',
            ),
        );
    }
