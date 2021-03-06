nosAction
#########

.. js:function:: $container.nosAction(action [, data ])

	Executes an action

	:param JSON action:

		JSON defines the action to execute.
		JSON must have an ``action`` key, can be :

		:nosTabs:            :js:attr:`nosAction.nosTabs`
		:nosDialog:          :js:attr:`nosAction.nosDialog`
		:confirmationDialog: :js:attr:`nosAction.confirmationDialog`
		:nosAjax:            :js:attr:`nosAction.nosAjax`
		:window.open:        :js:attr:`nosAction.windowOpen`
		:document.location:  :js:attr:`nosAction.documentLocation`
		:nosMediaVisualise:  :js:attr:`nosAction.nosMediaVisualise`
		:dialogPick:         :js:attr:`nosAction.dialogPick`

	:param JSON data: JSON contextual data. Used to replace placeholder in ``action`` by calling :js:func:`$.nosDataReplace`.

Actions list
************

.. contents::
	:local:
	:backlinks: top

.. _javascript/$/nosAction/nosTabs:

nosTabs
=======

.. js:attribute:: nosAction.nosTabs

	:action: ``nosTabs``
	:method: Any sub-function name of :js:func:`$container.nosTabs`.
	:tab:    First parameter passed to sub-function of :js:func:`$container.nosTabs`.
	:dialog: Second parameter passed to sub-function of :js:func:`$container.nosTabs`.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'nosTabs',
			method: 'add',
			tab: {
				url: 'path/url',
				label: 'A title',
				iconUrl: 'url/of/icon.png'
			},
			dialog: {
				width: 800,
				height: 400
			}
		});

nosDialog
=========

.. js:attribute:: nosAction.nosDialog

	:action: ``nosDialog``
	:dialog: Second parameter passed to :js:func:`nosDialog.open`.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'nosDialog',
			dialog: {
				ajax: true,
				contentUrl: 'path/url/,
				title: 'A title',
				width: 500,
				height: 200
			}
		});

confirmationDialog
==================

.. js:attribute:: nosAction.confirmationDialog

	A special form of :js:attr:`nosAction.nosDialog` for confirmation.

	:action: ``confirmationDialog``
	:dialog: Second parameter passed to :js:func:`nosDialog.open`.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'confirmationDialog',
			dialog: {
				contentUrl: 'path/url/,
				title: 'A title'
			}
		});


nosAjax
=======

.. js:attribute:: nosAction.nosAjax

	:action: ``nosAjax``
	:params: Settings of :js:func:`$container.nosAjax`.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'nosAjax',
			params: {
				url: 'path/url',
				method: 'POST',
				data: {
					id: '{{_id}}'
				)
			}
		}, {
			_id: 5
		});

window.open
===========

.. js:attribute:: nosAction.windowOpen

	Open a new browser window.

	:action: ``window.open``
	:url: URL of the new window.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'window.open',
			url: 'path/url'
		});

document.location
=================

.. js:attribute:: nosAction.documentLocation

	Redirects the browser window to a new URL.

	:action: ``document.location``
	:url: The new URL.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'document.location',
			url: 'path/url'
		});

nosMediaVisualise
=================

.. js:attribute:: nosAction.nosMediaVisualise

	This action has no parameters. It only depends on the data passed with action. See :js:func:`$.nosMediaVisualise`.

	:action: ``nosMediaVisualise``

	.. code-block:: js

		$(domContext).nosAction({
			action: 'nosMediaVisualise'
		}, {
			path: 'url/of/media/',
			image: true
		});

dialogPick
==========

.. js:attribute:: nosAction.dialogPick

	:action: ``dialogPick``
	:event: Name of the event to trigger.

	.. code-block:: js

		$(domContext).nosAction({
			action: 'dialogPick',
			'event' => 'event_name'
		});
