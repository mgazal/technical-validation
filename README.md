# technical-validation

Tool for the technical validation of custom code that extends the
[Alfresco](http://www.alfresco.com) open source document management system.  In other words it's an
automated AMP file checker (both repo AMPs and Share AMPs).

Important note: this tool is a beta, and has issues including:
 * Criteria that require manual followup
 * Criteria that are not yet checked at all
 * False positives
 * False negatives
 * Ugly output
 * Confusing output

That said, in experienced hands it can greatly expedite the process of technically validating an Alfresco extension,
by pinpointing potentially problematic areas of the code for further manual investigation.

## Dependencies
 1. [Java 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
 2. [neo4j 2.0+](http://www.neo4j.org/)
 3. [Ohcount](https://github.com/blackducksw/ohcount) (optional - without it some statistics will be missing from the
 reports generated by the tool)

Notes:
 * these dependencies should be installed via your OS package manager, where possible.  On Mac OSX, I strongly
   recommend [Homebrew](http://brew.sh/).
 * On Windows, do _not_ use the Neo4J executable installer as it is seemingly impossible to configure.  The zip
   distribution is a better choice.

## Configuration

Ensure "auto indexing" is enabled in Neo4J for the properties "name", "package" and "typename".  These are set in
the neo4j.properties file, as follows:
```INI
node_auto_indexing=true
node_keys_indexable=name,package,typename
```

## Installation

Download the [latest release](https://github.com/AlfrescoLabs/technical-validation/releases) and unzip the zip file
somewhere convenient.

## Running / usage

```shell
$ ./atv -h
 ---------------------------+-------------------------------+--------------------------------------------------------
  Parameter                 | Default Value                 | Description
 ---------------------------+-------------------------------+--------------------------------------------------------
  -s, --source SOURCE                                        Source folder (mandatory)
  -b, --binaries BINARIES                                    Binary folder or archive (mandatory)
  -n, --neo4j-url NEO4J_URL  http://localhost:7474/db/data/  URL of the Neo4J server to use (optional - see default)
  -w, --word-file FILE_NAME                                  Produce output as a Word document in the specified file
  -e, --edn-file FILE_NAME                                   Produce EDN output in the specified file
  -j, --json-file FILE_NAME                                  Produce JSON output in the specified file
  -h, --help                                                 This message
  At least one of -w, -e, or -j must be provided.
 ---------------------------+-------------------------------+--------------------------------------------------------
$
```

or on Windows:

```Batchfile
C:\atv> atv -h
 ---------------------------+-------------------------------+--------------------------------------------------------
  Parameter                 | Default Value                 | Description
 ---------------------------+-------------------------------+--------------------------------------------------------
  -s, --source SOURCE                                        Source folder (mandatory)
  -b, --binaries BINARIES                                    Binary folder or archive (mandatory)
  -n, --neo4j-url NEO4J_URL  http://localhost:7474/db/data/  URL of the Neo4J server to use (optional - see default)
  -w, --word-file FILE_NAME                                  Produce output as a Word document in the specified file
  -e, --edn-file FILE_NAME                                   Produce EDN output in the specified file
  -j, --json-file FILE_NAME                                  Produce JSON output in the specified file
  -h, --help                                                 This message
  At least one of -w, -e, or -j must be provided.
 ---------------------------+-------------------------------+--------------------------------------------------------
C:\atv>
```

The tool will write a lot of data to the Neo4J database specified in the command line parameters - it is strongly
recommended that that database be empty prior to each run of the tool.  It will also write the report file(s) to disk.
Other than that it will not modify anything else on the machine its run on (most especially the source code or binaries
of your extension - they are only read).

## Programmatic Access to the Tool

If you wish to use the tool as a library, it's available as a Maven artifact from [Clojars](https://clojars.org/org.alfrescolabs.alfresco-technical-validation):

[![version](https://clojars.org/org.alfrescolabs.alfresco-technical-validation/latest-version.svg)](https://clojars.org/org.alfrescolabs.alfresco-technical-validation)

The library's functionality is provided in the `alfresco-technical-validation.core` namespace, specifically
these functions:

```clojure
user=> (require '[alfresco-technical-validation.core :as atv])
nil
user=> (doc atv/validate)
-------------------------
alfresco-technical-validation.core/validate
([source binaries neo4j-url] [source binaries neo4j-url status-fn] [indexes status-fn])
  Validates the given source and binaries.
nil
user=> (doc atv/validate-and-write-report)
-------------------------
alfresco-technical-validation.core/validate-and-write-report
([source binaries neo4j-url report-filename] [source binaries neo4j-url report-filename status-fn] [indexes report-filename status-fn])
  Validates the given source and binaries, using the Neo4J server available at the given URL,
  writing the report to the specified Word document.
nil
```

As of v0.4.0, preliminary Java access has been added to the tool - please see
[this worked example](https://github.com/AlfrescoLabs/technical-validation-java-example) for details.

## Developer Information

[GitHub project](https://github.com/AlfrescoLabs/technical-validation)

[Bug Tracker](https://github.com/AlfrescoLabs/technical-validation/issues)

[![endorse](https://api.coderwall.com/pmonks/endorsecount.png)](https://coderwall.com/pmonks)

## License

Copyright © 2013,2014 Peter Monks (pmonks@gmail.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

This file is part of an unsupported extension to Alfresco.
