Crud
####

Configuration for :php:class:`Nos\\Orm\\Model`'s appdesk.

Associative array:

:controller_url: Url of the CRUD controller
:model:          Model handled by this controller
:environment_relation: Relation name. Allows to define a children / parent relationship.
:tab:            Tab informations, see :ref:`javascript/$/nosAction/nosTabs`
:views:          Optional. Views locations.
:layout:         Where fields are displayed on form. Optional if `layout_insert` and `layout_update` are defined.
:layout_insert:  Optional. Specific layout for insert. Will use ``layout`` as default value.
:layout_update:  Optional. Specific layour for update. Will use ``layout`` as default value.
:fields:         All fields displayed in the form.


environment_relation
********************

The ``environment_relation`` must contain a relation name of type ``Orm\\BelongsTo``.

It allows to use the ``GET['environment_id']`` in an action of this model.

It will be used to populate the column associated with the relation. Examples include:

- Add a page at a specific location inside the tree (with a pre-selected parent) ;
- Add a media in a specific folder ;
- Add a monkey inside a species ;
- Add an blog post inside a category.

**Some examples**:

.. code-block:: php

    <?php
    // Add a sub-page action
    'action' => array(
        'action' => 'nosTabs',
        'tab' => array(
            // The 'page_parent_id' will be populated with $_GET['environment_id'] from the action
            'url' => '{{controller_base_url}}insert_update?environment_id={{_id}}&context={{_context}}',
        ),
    ),


    // Add a media in this folder action
    'action' => array(
        'action' => 'nosTabs',
        'tab' => array(
            // The 'media_folder_id' will be populated with $_GET['environment_id'] from the action
            'url' => '{{controller_base_url}}insert_update?environment_id={{id}}',
        ),
    ),



tab
****

.. seealso:: :ref:`javascript/$/nosAction/nosTabs`


The ``tab`` configuration array has a special ``labels`` key, to handle several ``label`` depending on the case.

:insert:     Adding an new item
:blankSlate: Translating an existing item
:update:     Editing an existing item


- ``insert`` and ``update`` must contain plain ``string`` value ;
- ``update`` can either contain a plain ``string`` value, or a ``callable`` taking one argument: the ``$item`` ;
- The default value for ``labels.update`` is the item's title.


views
*****

:form:   View for the form (both insert and update). Default is ``nos::crud/form``.
:delete: View for the delete popup. Default is ``nos::crud/delete_popup``.
:insert: Optional. View for the insert form (will use ``form`` value as default)
:update: Optional. View for the update form (will use ``form`` value as default)


layout
******

``layout`` is a data passed to the parameters of the view.

There are two syntaxes, the normal (full) and a simplified form (because it's what we want to use 80% of the time).


Here is the **full normal syntax**:

.. code-block:: php

    <?php
    'layout' => array(
        'first_view' => array(
            'view' => 'nos::form/layout_standard',
            'params' => array(
                // View data
                'title' => '',
                'content' => '',
            ),
        ),
        'second_view' => array(
            'view' => 'noviusos_page::admin/page_form',
            // No 'params'
        ),
    ),


But Novius OS has a standard layout for the form, and that's what we want to use 80% of the time with the **simplified syntax**:

.. code-block:: php

    <?php
    'layout' => array(
        // View data
        'title' => '',
        'content' => '',
    ),

We only need to define the view data for the standard layout, and it will be wrapped like so:

.. code-block:: php

    <?php
    $layout = array(
        array(
            'view' => 'nos::form/layout_standard',
            'params' =>  $layout,
        ),
    );


.. seealso:: :doc:`/php/views/form`

.. _php/configuration/application/crud/fields:

fields
******

The ``fields`` syntax is based on an existing FuelPHP feature, which is used to configure form attributes for each column of a Model.

.. seealso::

    `FuelPHP documentation on Model::$_properties <http://docs.fuelphp.com/packages/orm/creating_models.html#propperties>`__

In addition to standard form fields, Novius OS has :term:`renderers <Renderer>`, which are a bit more advanced. For
instance, they allow to select a media, a page, a date...


Configuration example:

.. code-block:: php

	<?php
	return array(
		'name' => array(
			'label' => 'Text shown next to the field',
			'form' => array(
				'type' => 'text',
				'value' => 'Default value',
			),
			'validation' => array(),
	);


Standard fields
----------------

Bold text is the value for the ``type`` property.

* <input type="**text**">
* <input type="**password**">
* <**textarea**>
* <**select**>
* <input type="**radio**">
* <input type="**checkbox**">
* <input type="**submit**">
* <input type="**button**">
* <input type="**file**">

.. code-block:: php

	<?php
	return array(
		'gender' => array(
			'label' => 'Gender',
			'form' => array(
				'type' => 'select',
				'options' => array(
					'm' => 'Male',
					'f' => 'Female',
				)
			),
			'validation' => array('required'),
		),
	);


<button type="submit">
^^^^^^^^^^^^^^^^^^^^^^

* ``type = submit`` generates ``<input type="submit">``
* ``type = button`` generates ``<input type="button">``

The ``tag`` property can be used to force a precise HTML tag, it's useful for a ``submit`` button.

FuelPHP will automatically use the ``value`` as the button's text.

.. code-block:: php

	<?php
	return array(
		'save' => array(
			'form' => array(
				'type' => 'submit',
				'tag' => 'button',
				'value' => 'Save',
			),
		),
	);


Renderers (advanced fields)
---------------------------

The renderer list is available :ref:`in a dedicated page <php/renderers>`.

