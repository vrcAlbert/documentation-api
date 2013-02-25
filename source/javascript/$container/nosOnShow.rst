nosOnShow
#########

.. js:function:: $container.nosOnShow([method [, options [, ... ]]])

	Special API which delays the rendering of UI elements when they become visible.
	A lot of UI elements don’t initialise correctly when they are hidden (they can’t calculate sizes properly).

	This is a :term:`function with sub-functions`.

	:param mixed method: The sub-function name, ``show`` (default), ``one``  or ``bind``. If omitted, this is the first parameter of the default sub-function :js:func:`nosOnShow.show()`.
	:param mixed options: Parameters of the sub-function.

nosOnShow('show')
*****************

.. js:function:: nosOnShow.show()

	Triggers all functions bounded with :js:func:`nosOnShow.bind` for any children of ``$container``.

	.. warning::

		You have to actually show the element before calling this function.

	.. code-block:: js

		$(domContext).show().nosOnShow();

		// Or
		$(domContext).show().nosOnShow('show');


nosOnShow('one')
****************

.. js:function:: nosOnShow.one(callback)

	Binds a callback function which will be called only the one time (at the first display).

	:param function callback: A callback function.

	.. code-block:: js

		$(element).nosOnShow('one', function() {
			$(this).widget();
		});


nosOnShow('bind')
*****************

.. js:function:: nosOnShow.bind(callback)

	Binds a callback function which will be called each time that the element becomes visible.

	:param function callback: A callback function.

	.. code-block:: js

		$(element).nosOnShow('bind', function() {
			$(this).widgetRefresh(); // widgetRefresh don't exist, it's an example.
		});

