nosDialog
#########

.. js:function:: $container.nosDialog([method [, options [, ... ]]])

	Manage back-office's popup. This is a :term:`function with sub-functions`.

	:param mixed method: The sub-function name, ``open`` (default) or ``close``. If omit, this is the first parameter of the default sub-function :js:func:`nosDialog.open()`.
	:param mixed options: Parameters of the sub-function.

nosDialog('open')
*****************

.. js:function:: nosDialog.open(dialog)

	Open a popup. This is a wrapper of `Wijmo widget Dialog <http://wijmo.com/wiki/index.php/Dialog>`_.

	A popup can be created in three ways:

	* From an existing DOM element.
	* From an URL loaded into a ``iframe``.
	* Form an URL loaded into a ``<div>`` by AJAX request.

	Catch events dispatched by :js:func:`$.nosDispatchEvent`.

	:param JSON options:

		JSON that configure the popup. Same that ``$.wijdialog()`` with some differences:

		Some defaults options:

		:width: Container width minus 200 pixels.
		:height: Container height minus 100 pixels.
		:modal: True
		:captionButtons: Buttons ``pin``, ``refresh``, ``toggle``, ``minimize`` and ``maximize`` are hides.

		Additional options:

		:destroyOnClose: ``boolean``. Destroy popup when it's closed. Default ``true``.
		:ajax: ``boolean``. If ``true``, ``contentUrl`` is AJAX loaded rather than use ``iframe``. Default ``true``.
		:ajaxData: ``{}``. Data passed to AJAX request if ``ajax`` is ``true``.

	.. code-block:: js

		// Popup containing the HTML result of the AJAX request on contentUrl
		$(domContext).nosDialog('open',	{
			contentUrl: 'path/url',
			ajaxData: {
				foo: 'bar'
			},
			title: 'title of the popup',
			height: 400,
			width: 700
		});

		// Same as previous, without first parameter, open is the default sub-function
		$(domContext).nosDialog({
			contentUrl: 'path/url',
			ajaxData: {
				foo: 'bar'
			},
			title: 'title of the popup',
			height: 400,
			width: 700
		});

		// Popup containing an iframe width contentUrl href
		$(domContext).nosDialog({
			iframe: true
			contentUrl: 'path/url',
			title: 'title of the popup',
			height: 400,
			width: 700
		});

		// Popup containing <div> with the id 'id_de_div'
		$('#id_de_div').nosDialog({
			title: 'title of the popup',
			height: 400,
			width: 700
		});

nosDialog('close')
******************

.. js:function:: nosDialog.close()

	Close current popup (compared to the dialog where is the DOM element in jQuery container).

	.. code-block:: js

		$(domContext).nosDialog('close');
