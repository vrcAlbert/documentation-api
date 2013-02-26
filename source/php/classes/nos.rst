Nos
####

.. php:namespace:: Nos

.. php:class:: Nos

	Provide static methods useful in Novius OS.


Entry points
------------

.. php:attr:: entry_point

	The Novius OS entry point. Equal to one of the following constants.

.. php:const:: ENTRY_POINT_ADMIN
.. php:const:: ENTRY_POINT_FRONT
.. php:const:: ENTRY_POINT_404
.. php:const:: ENTRY_POINT_INSTALL


::main_controller()
-------------------

.. php:staticmethod:: main_controller()

	:returns: Instance of main :term:`controller <Controller>`.

::hmvc()
--------

.. php:staticmethod:: hmvc($where, $args = null)

	:param mixed $where: Route for the request.
	:param array $args: The method parameters.

	Execute a :term:`HMVC` request.

::parse_wysiwyg()
-----------------

.. php:staticmethod:: parse_wysiwyg($content)

	:param string $content: A :php:class:`Nos\\Model_Wysiwyg` content.
	:returns: Prepare wysiwyg content for display.

	| Replace enhancers by theirs content
	| Replace :php:class:`Model_Page` and :php:class:`Model_Media` IDs by theirs URLs
	| Add URL prefix on anchors (for work with ``base_href``).
