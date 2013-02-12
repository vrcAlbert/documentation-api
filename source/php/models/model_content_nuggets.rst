Model_Content_Nuggets
#####################

.. php:class:: Model_Content_Nuggets

	| Extend :php:class:`Model`.
	| Belongs to the namespace :php:ns:`Nos`

.. todo::

	* liens vers reference glossaire de data catchers
	* liens vers reference glossaire de content nugget

Constantes
**********

.. php:const:: DEFAULT_CATCHER

	Value a default ``data catcher`` for ``content_catcher`` column.


Columns
*******

:content_id: Model_Content_Nuggets primary key.
:content_catcher: ``Data catcher`` name.
:content_model_name: Name of the model which are the outcome ``content nuggets``.
:content_model_id: ID of the model which are the outcome ``content nuggets``.
:content_data: The ``content nuggets``. An associative array serialize.
