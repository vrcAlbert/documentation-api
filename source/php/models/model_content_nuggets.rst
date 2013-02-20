Model_Content_Nuggets
#####################

.. php:namespace:: Nos

.. php:class:: Model_Content_Nuggets

	Extends :php:class:`Nos\\Orm\\Model`.

.. todo::

	* liens vers reference glossaire de data catchers
	* liens vers reference glossaire de content nugget

Constants
*********

.. php:const:: DEFAULT_CATCHER

	Default value for the ``content_catcher`` column.


Columns
*******

:content_id:         Model_Content_Nuggets primary key.
:content_catcher:    ``Data catcher`` name.
:content_model_name: Name of the model this ``content nuggets`` originates from.
:content_model_id:   ID of the model this ``content nuggets`` originates from.
:content_data:       The ``content nuggets``. Stored as a serialized associative array.
