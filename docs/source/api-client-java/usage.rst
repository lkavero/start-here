Command line options for api-client-java
----------------------------------------

To command line is now the best place for help. Executing without any parameters::

  java -jar target/genomics-tools-client-java-v1beta2.jar

will print out all the available commands. To get help on a specific command, 
append the command followed by ``help``. For example to get help on the searchreads command::

  java -jar target/genomics-tools-client-java-v1beta2.jar searchreads help

All the request types map to Genomics API calls. You can read the
`API documentation <https://developers.google.com/genomics/v1beta2/reference>`_
for more information about the various objects, and what each method is doing.



The custom command
~~~~~~~~~~~~~~~~~~

If you wish to call an API method that doesn't have a pre-defined request type, 
or if you wish to pass in additional JSON fields that aren't supported with the 
existing options, then you can issue a fully custom request with the following parameters:

--custom_endpoint  Required. The API endpoint to query. This is relative 
                   to the base URL and shouldn't start with a ``/`` Example: ``readgroupsets/search``.
--custom_method    The HTTP method to query with. Defaults to ``POST``. Other valid examples are 
                   ``GET``, ``PATCH``, ``DELETE``.
--custom_body      If the API endpoint you are hitting requires a HTTP body, use this 
                   parameter to pass in a JSON object as a string. It should look something like ``{"key": "value"}``
                     
Putting these pieces together, if you wanted to do a readsets search with name filtering 
(which isn't supported through the other options) you could do so with this query::

  java -jar target/genomics-tools-client-java-v1beta2.jar custom --custom_endpoint "readgroupsets/search" --custom_body '{"datasetIds": ["10473108253681171589"], "name": "NA1287"}' --fields "readGroupSets(id,name)" --pretty_print

If instead you wanted to make a ``GET`` call, your custom request could look like this::

  java -jar target/genomics-tools-client-java-v1beta2.jar custom --custom_endpoint "readgroupsets/CMvnhpKTFhD04eLE-q2yxnU" --custom_method "GET" --fields "id,name" --pretty_print
