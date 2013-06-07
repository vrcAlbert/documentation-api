nosTabs
#######

.. js:function:: $container.nosTabs([method [, options [, ... ]]])

	Manages back-office's tabs. This is a :term:`function with sub-functions`.

	:param mixed method: The sub-function name, ``open`` (default), ``add``, ``close``, ``update`` or ``current``. If omitted, this is the first parameter of the default sub-function :js:func:`nosTabs.open()`.
	:param mixed options: Parameters of the sub-function.

nosTabs('open')
***************

.. js:function:: nosTabs.open(tab [, dialogOptions ])

	Open a new tab or re-open an existing tab if it has the same URL.

	:param mixed tab: JSON definition of tab.

		:url:          Required. Tab URL.
		:iframe:       If true, open tab in an iframe. Default ``false``.
		:label:        Tab label.
		:labelDisplay: If false, don't display the label, only the icon. Default ``true``.
		:iconUrl:      Icon URL.
		:iconSize:     Icon size in pixel (square icon). Default 16.

	:param JSON dialogOptions: Within a popup, a tab will rather open another new popup instead (by calling :js:func:`$container.nosDialog`). This parameter set options for :js:func:`$container.nosDialog`.

	.. code-block:: js

		$(domContext).nosTabs('open', {
			url: 'path/url',
			iframe: false,
			label: 'title',
			labelDisplay: true,
			iconUrl: 'path/icon.png',
			iconSize: 16
		});

		// Call simplified
		$(domContext).nosTabs({
			url: 'path/url',
			iframe: false,
			label: 'title',
			labelDisplay: true,
			iconUrl: 'path/icon.png',
			iconSize: 16
		});

nosTabs('add')
**************

.. js:function:: nosTabs.add(tab [, dialogOptions, position ])

	Adds a new tab, even if an existing has the same URL.

	:param mixed tab: JSON definition of tab.

		:url:          Required. Tab URL.
		:iframe:       If true, open tab in an iframe. Default ``false``.
		:label:        Tab label.
		:labelDisplay: If false, don't display the label, only the icon. Default ``true``.
		:iconUrl:      Icon URL.
		:iconSize:     Icon size in pixel (square icon). Default 16.

	:param string position: Position of the new tab. Can be ``end``, ``before`` or ``after`` the current tab of the js:data::`jQuery $container <$container>`.
	:param JSON dialogOptions: If DOM element in jQuery container is in popup, open a new popup by calling :js:func:`$container.nosDialog` instead of a tab. This parameter set options for :js:func:`$container.nosDialog`.

	.. code-block:: js

		$(domContext).nosTabs(
			'add',
			{
				url: 'path/url',
				iframe: false,
				label: 'title',
				labelDisplay: true,
				iconUrl: 'path/icon.png',
				iconSize: 16
			},
			'end'
		);

nosTabs('close')
****************

.. js:function:: nosTabs.close()

	Close current tab (compared to the tab where is the DOM element in jQuery container).

	.. code-block:: js

		$(domContext).nosTabs('close');

nosTabs('update')
*****************

.. js:function:: nosTabs.update(tab)

	Update current js:data::`$container` tab. Can load a new URL.

	:param mixed tab: JSON definition of tab.

		:url:          Required. Tab URL.
		:label:        Tab label.
		:labelDisplay: If false, don't display the label, only the icon. Default ``true``.
		:iconUrl:      Icon URL.
		:iconSize:     Icon size in pixel (square icon). Default 16.
		:reload:       If true and ``url`` is set, load the new URL in the current tab. Default ``false``.

	.. code-block:: js
	   :emphasize-lines: 7

		$(domContext).nosTabs('update', {
			url: 'path/url',
			label: 'Title',
			labelDisplay: true,
			iconUrl: 'path/icon.png',
			iconSize: 16
			reload: true
		});

nosTabs('reload')
*****************

.. js:function:: nosTabs.reload()

	Reload current js:data::`$container` tab.

	.. code-block:: js

    		$(domContext).nosTabs('reload');

nosTabs('current')
******************

.. js:function:: nosTabs.current(tab)

	:returns: Index of the current js:data::`$container` tab.

	.. code-block:: js

		var current = $(domContext).nosTabs('current');

