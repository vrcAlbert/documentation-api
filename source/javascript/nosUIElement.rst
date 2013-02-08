nosUIElement
############

.. js:function:: $.nosUIElement(element [, data ])

	:param JSON element: JSON definition of the element to create.

		:type: ``string``. ``button`` (default) or ``link``. See :js:fun:`$container.nosFormUI` for buttons ``data``, those of links are almost the same.
		:label: ``string``. Element label.
		:action: ``{}``. Action bound to click event. See :js:func:`$container.nosAction`.
		:bind: ``{}``. Event(s) bound to element. Voir `$().bind() <http://api.jquery.com/bind/>`_.
		:disabled: ``boolean``. If ``true``, the element is disabled.
		:menu: ``{}``. If set, bind a context menu to element.

			:menus: ``[{}]``. Array containing each menu line.

				:action: ``{}``. Action bound to click event of menu line. See :js:func:`$container.nosAction`.
				:content: ``string``. HTML content of the menu line.
				:label: ``string``. Label of the menu line.
				:icon: Icon name (See `icons names of jQuery UI <http://jqueryui.com/themeroller/>`_) without the ``ui-icon-`` prefix.
				:iconClasses: CSS classes of icon.
				:iconUrl: Icon URL.

			:options: ``{}``. Settings for `Wijmo widget wijmenu <http://wijmo.com/wiki/index.php/Menu>`_.

	:param JSON data: Data attached to element and passed to action. See :js:func:`$container.nosAction`.

	:returns: A DOM element detach from DOM.

	.. code-block:: js

		$.nosUIElement({
			type: 'button',
			label: 'A button'
		},
		{
			id: 5
			foo: 'bar'
		});
