# technical-validation

Tool for the technical validation of custom code that extends the
[Alfresco](http://www.alfresco.com) open source document management system.

## Dependencies
 1. [Java 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
 2. [neo4j 2.0+](http://www.neo4j.org/)
 3. [Ohcount](https://github.com/blackducksw/ohcount)

Note: these dependencies should be installed via your OS package manager, where possible.  On Mac OSX,
I strongly recommend [Homebrew](http://brew.sh/).

## Installation

Download the [latest release](https://github.com/AlfrescoLabs/technical-validation/releases) and unzip the zip file
somewhere convenient.

## Running / usage

```shell
$ ./atv -h
 ------------------------------+-------------------------------+--------------------------------------------------------
  Parameter                    | Default Value                 | Description
 ------------------------------+-------------------------------+--------------------------------------------------------
  -s, --source SOURCE                                            Source folder (mandatory)
  -b, --binaries BINARIES                                        Binary folder or archive (mandatory)
  -n, --neo4j-url NEO4J_URL      http://localhost:7474/db/data/  URL of the Neo4J server to use (optional - see default)
  -r, --report-file REPORT_FILE                                  The filename of the output report (mandatory)
  -h, --help                                                     This message
 ------------------------------+-------------------------------+--------------------------------------------------------
$ 
```

or on Windows:

```Batchfile
C:\atv-0.1.0> atv -h
 ------------------------------+-------------------------------+--------------------------------------------------------
  Parameter                    | Default Value                 | Description
 ------------------------------+-------------------------------+--------------------------------------------------------
  -s, --source SOURCE                                            Source folder (mandatory)
  -b, --binaries BINARIES                                        Binary folder or archive (mandatory)
  -n, --neo4j-url NEO4J_URL      http://localhost:7474/db/data/  URL of the Neo4J server to use (optional - see default)
  -r, --report-file REPORT_FILE                                  The filename of the output report (mandatory)
  -h, --help                                                     This message
 ------------------------------+-------------------------------+--------------------------------------------------------
C:\atv-0.1.0> 
```

The tool will write a lot of data to the Neo4J database specified in the command line parameters - it is strongly
recommended that that database be empty prior to each run of the tool.  It will also write the report file (in Word
.docx format) to disk.  Other than that it will not modify anything else on the machine its run on (most especially
the source code or binaries of your extension - they are only read).

## Developer Information

[GitHub project](https://github.com/AlfrescoLabs/technical-validation)

[Bug Tracker](https://github.com/AlfrescoLabs/technical-validation/issues)

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
