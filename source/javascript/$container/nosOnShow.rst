nosOnShow
#########

.. js:function:: $container.nosOnShow([method [, options [, ... ]]])

	Special API which delays the rendering of UI elements when they are visible.
	A lot of UI elements don’t initialise correctly when they are hidden (they can’t calculate sizes properly).

	This is a :term:`function with sub-functions`.

	:param mixed method: The sub-function name, ``show`` (default), ``one``  or ``bind``. If omit, this is the first parameter of the default sub-function :js:func:`nosOnShow.show()`.
	:param mixed options: Parameters of the sub-function.

nosOnShow('show')
*****************

.. js:function:: nosOnShow.show()

	Trigger all functions bounded with :js:func:`nosOnShow.bind` by children elements of the DOM element in jQuery container.

	.. warning::

		You have to show element before call this function.

	.. code-block:: js

		$(domContext).show().nosOnShow();

		// Or
		$(domContext).show().nosOnShow('show');


nosOnShow('one')
****************

.. js:function:: nosOnShow.one(callback)

	Bind a function which will be called just at the first display.

	:param function callback: A callback function.

	.. code-block:: js

		$(element).nosOnShow('one', function() {
			$(this).widget();
		});


nosOnShow('bind')
*****************

.. js:function:: nosOnShow.bind(callback)

	Bind a function which will be called each time that the element toggle visible.

	:param function callback: A callback function.

	.. code-block:: js

		$(element).nosOnShow('bind', function() {
			$(this).widgetRefresh(); // widgetRefresh don't exist, it's an example.
		});

