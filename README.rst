Confirm
=======

.. image:: https://api.travis-ci.org/louib/confirm.svg

Simple Python configuration file management.

Confirm validates a configuration file (.INI or YAML format) against a YAML
configuration schema.

Example schema file
-------------------

.. code:: yaml

  "system":
      "name":
          "required": true
          "description": "Name of the system associated with the server."
          "type": "str"
  "http_server":
      "listen":
          "required": true
          "type": "str"
          "description": "Listening address of the HTTP server."
          "default": "localhost"
      "port":
          "required": true
          "type": "int"
          "default": 8088
          "description": "Port of the HTTP server."
  "threading":
      "initial_pool_size":
          "description": "Initial number of threads in the thread pool."
          "type": "int"
          "default": 10
      "maximum_pool_size":
          "description": "Maximum number of threads in the thread pool."
          "type": "int"
          "default": 100
          "deprecated": true


Usage
-----

.. code:: bash

  $ confirm validate examples/confirm.yaml project.conf
  Error   : Missing required section system.
  Error   : Missing required section http_server.
  Warning : Deprecated option maximum_pool_size is present in section threading!


Confirm can also be used for validation as a Python library:

.. code:: python

  from confirm.validator import load_validation_from_files
  ...

    result = load_validation_from_files(schema_file_path, config_file_path)
    result.validate()
    print(result.is_valid())


License
-------
MIT License.
