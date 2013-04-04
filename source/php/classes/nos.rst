Nos
####

.. php:namespace:: Nos

.. php:class:: Nos

	Provides static methods useful in Novius OS.


Entry points
------------

.. php:attr:: entry_point

	The Novius OS entry point. Equal to one of the following constants.

.. php:const:: ENTRY_POINT_ADMIN
.. php:const:: ENTRY_POINT_FRONT
.. php:const:: ENTRY_POINT_404
.. php:const:: ENTRY_POINT_INSTALL
.. php:const:: ENTRY_POINT_OIL

.. versionadded:: 0.2.0.1

.. _php/classes/nos/main_controller:

::main_controller()
-------------------

.. php:staticmethod:: main_controller()

	:returns: Instance of the main :term:`controller <Controller>`.

::hmvc()
--------

.. php:staticmethod:: hmvc($where, $args = null)

	:param mixed $where: Route for the request.
	:param array $args: The method parameters.

	Executes an :term:`HMVC` request.

::parse_wysiwyg()
-----------------

.. php:staticmethod:: parse_wysiwyg($content)

	:param string $content: A :php:class:`Nos\\Model_Wysiwyg` content.
	:returns: Prepare wysiwyg content for display.

	| Replace enhancers by their content.
	| Replace :php:class:`Model_Page` and :php:class:`Model_Media` IDs by theirs URLs
	| Wysiwyg anchors are processed in case the href attribute begin with # :
	* If it begins with only one # then the href will be prefixed by the page url.
	* If if begins with two ## then it is transformed to only one #.