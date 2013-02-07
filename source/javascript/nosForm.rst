nosFormUI
#########

.. js:function:: $context.nosFormUI()

	Will perform UI enhancements on DOM elements (which are children of the DOM element in jQuery)
	using `Wijmo <http://wijmo.com/wiki/index.php/Main_Page>`_ and `jQuery UI <http://http://api.jqueryui.com/>`_ widgets.

	Element with CSS class ``.notransform`` will not be formatting.

	:input text: Using `widget wijtextbox <http://wijmo.com/wiki/index.php/Textbox>`_.
	:select: Using `widget wijdropdown <http://wijmo.com/wiki/index.php/Dropdown>`_.
	:checkbox: Using `widget wijcheckbox <http://wijmo.com/wiki/index.php/Checkbox>`_.
	:radio: Using `widget wijradio <http://wijmo.com/wiki/index.php/Radio>`_.
	:expander: | Elements with CSS class ``.expander`` using `widget wijexpander <http://wijmo.com/wiki/index.php/Expander>`_.
	  		   | You can set HTML attribut ``data-wijexpander-options`` contening a JSON for additional settings.
	:accordion: Elements with CSS class ``.accordion`` using `widget wijaccordion <http://wijmo.com/wiki/index.php/Accordion>`_.
	:submit: | Using `widget button <http://api.jqueryui.com/button/>`_.
		     | You can set HTML attributs ``data-`` for additional settings:

		:red: Make red button.
		:icons: ``{}``. Define icons for button.
		:icon: Define left icon name (See `icons names of jQuery UI <http://jqueryui.com/themeroller/>`_).
		:iconClasses: Define CSS classes for left icon.
		:iconUrl: Define URL of the left icon.

	.. code-block:: js

		$(domContext).nosFormUI();

nosFormAjax
###########

.. js:function:: $context.nosFormAjax()

	Will use the `jquery-form <http://malsup.com/jquery/form/>`_ plugin to submit the form (the DOM element in jQuery or children forms)
	using Ajax rather than the native browser action.

	Data type in return will be by default ``json``, and callbacks functions ``success`` and ``error`` call :js:func:`$context.nosAjaxSuccess` et :js:func:`$context.nosAjaxError`.

	.. code-block:: js

		$(domContext).nosFormAjax();


nosFormValidate
###############

.. js:function:: $context.nosFormValidate()

	Will use the `jquery-validation <http://docs.jquery.com/Plugins/Validation>`_ plugin to perform inline validation on the form (the DOM element in jQuery or children forms).
	It’s already configured to display error messages nicely, and take into account some specificity from the UI enhancements (like the accordion).

	Most forms are using it, since it’s part of the standard form layout.

	.. code-block:: js

		$(domContext).nosFormValidate({});

