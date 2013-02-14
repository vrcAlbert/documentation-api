nosToolbar
##########

.. js:function:: $container.nosToolbar([method [, options [, ... ]]])

	Manage back-office's toolbars. This is a :term:`function with sub-functions`.

	:param mixed method: The sub-function name, ``add`` (default) or ``create``. If omit, this is the first parameter of the default sub-function :js:func:`nosToolbar.add()`.
	:param mixed options: Parameters of the sub-function.

nosToolbar('add')
*****************

.. js:function:: nosToolbar.add(element [, right_side ])

	Add element to toolbar on which depends the DOM element in jQuery container. If no toolbar exist, create one on the fly.

	:param mixed element: Can be HTML code, a DOM element or a jQuery container.
	:param boolean right_side: Default ``false``, if ``true`` element added at the right side of the toolbar.

	.. code-block:: js

		$(domContext).nosToolbar('add', element, right_side);

		\\ or
		$(domContext).nosToolbar(element, right_side);

		\\ Add a button, right side of toolbar
		$(domContext).nosToolbar('<button>Exemple</button>', true);

		\\ Add a link, left side of toolbar
		var $a = $('<a href="#">Exemple</a>');
		$(domContext).nosToolbar($a);

nosToolbar('create')
********************

.. js:function:: nosToolbar.create()

	Add a toolbar above the DOM element in jQuery container.

	.. code-block:: js

		$(domContext).nosToolbar('create');
