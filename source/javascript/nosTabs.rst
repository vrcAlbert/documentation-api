nosTabs
#######

.. js:function:: $context.nosTabs([method [, options [, ... ]]])

	Manage back-office's tabs. This is a :ref:`javascript/sub_function`.

	:param mixed method: The sub-function name, ``open`` (default), ``add``, ``close``, ``update`` or ``current``. If omit, this is the first parameter of the default sub-function :js:func:`nosTabs.open()`.
	:param mixed options: Parameters of the sub-function.

nosTabs('open')
***************

.. js:function:: nosTabs.open(tab)

	Open a new tab or re-open an existing tab if it has the same URL.

	:param mixed tab: JSON definition of tab.

	.. code-block:: js

		$(domContext).nosTabs('open', {
			url: 'path/url', // Required. Tab URL.
			iframe: false, // If true, open tab in an iframe.
			label: 'title', // Tab label.
			labelDisplay: true, // If false, don't display the label, only the icon.
			iconUrl: 'path/icon.png', // Icon URL.
			iconSize: 16 // Icon size in pixel (square icon).
		});

		// Call simplified
		$(domContext).nosTabs({
			url: 'une/url',
			iframe: false,
			label: 'un titre',
			labelDisplay: true,
			iconUrl: 'url/de/l/icon.png',
			iconSize: 16
		});

nosTabs('add')
**************

.. js:function:: nosTabs.add(tab)

	Add a new tab, even if an existing has the same URL.

	:param mixed tab: JSON definition of tab.
	:param string position: Position of the new tab. Can be ``end``, ``before`` or ``after`` the current tab (compared to the tab where is the DOM element in jQuery).

	.. code-block:: js

		$(domContext).nosTabs(
			'add',
			{
				url: 'path/url', // Required. Tab URL.
				iframe: false, // If true, open tab in an iframe.
				label: 'title', // Tab label.
				labelDisplay: true, // If false, don't display the label, only the icon.
				iconUrl: 'path/icon.png', // Icon URL.
				iconSize: 16 // Icon size in pixel (square icon).
			},
			'end'
		);

nosTabs('close')
****************

.. js:function:: nosTabs.close()

	Close current tab (compared to the tab where is the DOM element in jQuery).

	.. code-block:: js

		$(domContext).nosTabs('close');

nosTabs('update')
*****************

.. js:function:: nosTabs.update(tab)

	Update current tab (compared to the tab where is the DOM element in jQuery). Can load a new URL.

	:param mixed tab: JSON definition of tab.

	.. code-block:: js
	   :emphasize-lines: 7

		$(domContext).nosTabs('update', {
			url: 'path/url', // Required. Tab URL.
			label: 'title', // Tab label.
			labelDisplay: true, // If false, don't display the label, only the icon.
			iconUrl: 'path/icon.png', // Icon URL.
			iconSize: 16 // Icon size in pixel (square icon).
			reload: false // If true and ``url`` is set, load the new URL in the current tab.
		});

nosTabs('current')
******************

.. js:function:: nosTabs.current(tab)

	:returns: Index of the current tab (compared to the tab where is the DOM element in jQuery).

	.. code-block:: js

		var current = $(domContext).nosTabs('current');

