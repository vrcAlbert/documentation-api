nosUIElement
############

.. js:function:: $.nosUIElement(element [, data ])

	:param JSON element: JSON definition of the element to create.

		:type:     ``string``. ``button`` (default) or ``link``. See :js:func:`$container.nosFormUI` for buttons ``data``, those of links are almost the same.
		:label:    ``string``. Element label.
		:action:   ``{}``. Action bound to the click event. See :js:func:`$container.nosAction`.
		:bind:     ``{}``. Event(s) bound to the element. See `$().bind() <http://api.jquery.com/bind/>`__.
		:disabled: ``boolean``. If ``true``, the element is disabled.
		:menu:     ``{}``. If set, binds a context menu to element.

			:menus: ``[{}]``. Array containing each menu line.

				:action: ``{}``. Action bound to the click event of the menu line. See :js:func:`$container.nosAction`.
				:content: ``string``. HTML content of the menu line.
				:label: ``string``. Label of the menu line.
				:icon: Icon name (See `icons name of jQuery UI <http://jqueryui.com/themeroller/>`__) without the ``ui-icon-`` prefix.
				:iconClasses: CSS classes of icon.
				:iconUrl: Icon URL.

			:options: ``{}``. Settings for `Wijmo widget wijmenu <http://wijmo.com/wiki/index.php/Menu>`__.

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

.. note:: ``content`` and ``label`` are exclusive. You don't need both. Same goes for the ``icon`` (either use a name, CSS classes or an URL).
