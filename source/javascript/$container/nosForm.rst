nosFormUI
#########

.. js:function:: $container.nosFormUI()

	Will perform UI enhancements on DOM elements on all the children of js:data::`$container` using
	`Wijmo <http://wijmo.com/wiki/index.php/Main_Page>`__ and `jQuery UI <http://http://api.jqueryui.com/>`__ widgets.

	Element with a ``.notransform`` CSS class will be left unchanged.

	:input text: Using the `wijtextbox widget <http://wijmo.com/wiki/index.php/Textbox>`__.
	:select:     Using the `wijdropdown widget <http://wijmo.com/wiki/index.php/Dropdown>`__.
	:checkbox:   Using the `wijcheckbox widget <http://wijmo.com/wiki/index.php/Checkbox>`__.
	:radio:      Using the `wijradio widget <http://wijmo.com/wiki/index.php/Radio>`__.
	:expander:   | Elements with the ``.expander`` CSS class  using `wijexpander widget <http://wijmo.com/wiki/index.php/Expander>`__.
	  		     | You can set options with the ``data-wijexpander-options`` HTML attribute (JSON for additional settings).
	:accordion:  Elements with CSS class ``.accordion`` using `wijaccordion widget <http://wijmo.com/wiki/index.php/Accordion>`__.
	:submit:     | Using the `button widget <http://api.jqueryui.com/button/>`__.
		         | You can set options with the ``data-`` HTML attributes (additional settings).

		:red: Makes the button red.
		:icons: ``{}``. Define icons for the button.
		:icon: Defines the left icon using a name (See `icons names of jQuery UI <http://jqueryui.com/themeroller/>`_).
		:iconClasses: Defines the left icon CSS classes for left icon.
		:iconUrl: Define URL of the left icon.

	.. code-block:: js

		$(domContext).nosFormUI();

nosFormAjax
###########

.. js:function:: $container.nosFormAjax()

	Will use the `jquery-form <http://malsup.com/jquery/form/>`__ plugin to submit any form inside js:data::`$container`
	using Ajax rather than the native browser action.

	The default response data type is ``json``, and the ``success`` and ``error`` callbacks functions will call
	:js:func:`$container.nosAjaxSuccess` and :js:func:`$container.nosAjaxError`.

	.. code-block:: js

		$(domContext).nosFormAjax();


nosFormValidate
###############

.. js:function:: $container.nosFormValidate()

	Will use the `jquery-validation <http://docs.jquery.com/Plugins/Validation>`__ plugin to perform inline
	validation on any form inside js:data::`$container`.

	It’s already configured to display error messages nicely, and take into account some specificity from the UI
	enhancements (like the accordion).

	Most forms are using it, since it’s part of the form's standard layout.

	.. code-block:: js

		$(domContext).nosFormValidate({});

