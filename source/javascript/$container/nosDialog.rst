nosDialog
#########

.. js:function:: $container.nosDialog([method [, options [, ... ]]])

	Manages back-office's popup. This is a :term:`function with sub-functions`.

	:param mixed method:  The sub-function name, ``open`` (default) or ``close``. If omitted this is the first parameter of the default sub-function :js:func:`nosDialog.open()`.
	:param mixed options: Parameters of the sub-function.

nosDialog('open')
*****************

.. js:function:: nosDialog.open(dialog)

	Opens a popup. This is a wrapper of `Wijmo widget Dialog <http://wijmo.com/wiki/index.php/Dialog>`__.

	A popup can be created in three ways:

	* From an existing DOM element.
	* From an URL loaded into an ``iframe``.
	* Form an URL loaded into a ``<div>`` from an AJAX request.

	Catch events dispatched by :js:func:`$.nosDispatchEvent`.

	:param JSON options:

		JSON that configures the popup. Same as ``$.wijdialog()`` with some differences:

		Some defaults options:

		:width: Container width minus 200 pixels.
		:height: Container height minus 100 pixels.
		:modal: True
		:captionButtons: Buttons ``pin``, ``refresh``, ``toggle``, ``minimize`` and ``maximize`` are hidden.

		Additional options:

		:destroyOnClose: ``boolean``. Destroys the popup when it's closed. Default ``true``.
		:ajax: ``boolean``. If ``true``, ``contentUrl`` is loaded using AJAX rather than using an ``iframe``. Default ``true``.
		:ajaxData: ``{}``. Data passed to the AJAX request (if ``ajax`` is ``true``).

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

	Closes the current popup dialog (i.e. from the current js:data::`DOM container <$container>`).

	.. code-block:: js

		$(domContext).nosDialog('close');
