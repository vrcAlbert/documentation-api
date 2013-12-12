Application_Generator Class
###########################

.. php:namespace:: Nos\AppWizard

.. php:class:: Application_Generator

.. php:staticmethod:: generate($config, $input)

    :param array $config:

        :generation_path: Location of all files needed for the application generation
        :folders: Folders to create when generating an application
        :files: callback function

            :param string $root_dir: Root directory where all files must be generated (likely to be the generated application path)
            :param array $data: Form input
            :param array $config: Generator configuration

            :returns: Array of array, each array defining a file to be generated:

                :template: Generate from this view
                :data: View data
                :destination:

        :category_types:

            | Key => value array defining categories (fields group type). Key is the category identifier.
            | Value is an array containing:

            :label:

        :fields: Key => value array defining field types. Key is the field type identifier. Value is an array containing:

            :label:
            :on_model_properties: Will the field create an associated model property.

    :param array $input: Form input


.. php:staticmethod:: indent($pre, $str)

    View helper that allows to keep a consistent indentation when generating code.

    :param string $pre: Piece of string to be appended before each line (likely to be spaces)
    :param string $str: Code to be indented


.. php:staticmethod:: generateFolders($root_dir, $folders)

    Generates folders from a list of folder paths

    :param string $root_dir: Root directory where all folders are generated
    :param array $folders: List of folder paths


.. php:staticmethod:: generateFiles($root_dir, $config, $input)

    Generates applications files (models, controllers, view), from information on the configuration file and the form
    values.

    :param string $root_dir: Root director (likely to be the generated application directory)
    :param array $config: Configuration
    :param array $input: Form values