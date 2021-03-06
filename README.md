SonarQube Delphi
================

This is the SonarQube Delphi Plugin.

This plugin was originally a [Sabre Airline Solutions](http://www.sabreairlinesolutions.com/home/) donation.

<!---
[![Build Status](https://travis-ci.org/fabriciocolombo/sonar-delphi.svg?branch=master)](https://travis-ci.org/fabriciocolombo/sonar-delphi)
--->

<!---
Project homepage:
http://docs.sonarqube.org/display/PLUG/JavaScript+Plugin

Issue tracking:
http://jira.sonarsource.com/browse/SONARJS
--->

Steps to Analyze a Delphi Project
------------------------------------------------

1. Install SonarQube Server (see [Setup and Upgrade](http://docs.sonarqube.org/display/SONAR/Setup+and+Upgrade) for more details)
2. Install one of the supported [Runners](#supported-runners) (see below) and be sure you can call it from the directory where you have your source code
3. Install Delphi Plugin (see [Installing a Plugin](http://docs.sonarqube.org/display/SONAR/Installing+a+Plugin)  for more details). By default Java Plugin is provided out of the box with SonarQube.
4. Check the sample project corresponding to your Runner to know which config file you need to create. You can find the samples in `sonar-delphi/samples`.
5. Run your Analyzer command from the project root dir
6. Follow the link provided at the end of the analysis to browse your project's quality in SonarQube UI (see: [Browsing SonarQube](http://docs.sonarqube.org/display/SONAR/Browsing+SonarQube))

Supported Runners
----------------------------
 To run an analysis of your Java project, you can use the following Runners:

* [SonarQube Runner](http://docs.sonarqube.org/display/SONAR/Installing+and+Configuring+SonarQube+Runner): recommended for all non-Maven projects
* [Maven](http://docs.sonarqube.org/display/SONAR/Installing+and+Configuring+Maven): recommended for all projects built with Maven
* [SonarQube Ant Task](http://docs.sonarqube.org/display/SONAR/Installing+and+Configuring+Ant+SonarQube+Task): to integrate with projects built with Ant
* [Gradle](http://docs.sonarqube.org/display/SONAR/Analyzing+with+Gradle): to integrate with projects built with Gradle


Implemented Features
------------------------------------------

* Counting lines of code, statements, number of files
* Counting number of classes, number of packages, methods, accessors
* Counting number of public API (methods, classes and fields)
* Counting comments ratio, comment lines (including blank lines)
* CPD (code duplication, how many lines, block and in how many files)
* Code Complexity (per method, class, file; complexity distribution over methods, classes and files)
* LCOM4 and RFC
* Code colorization
* Unit tests reports
* Assembler syntax in grammar
* Include statement
* Parsing preprocessor statements
* Rules
* Code coverage reports
* Source code highlight for unit tests
* �Dead� code recognition
* Unused files recognition

Code Assumptions
----------------------------------

* Grammar is NOT case insensitive, but Delphi code is. Plugin deals with it by DelphiSourceSanitizer class, which feeds ANTLR parser lowercase characters (the �LA� method)
* Number of classes includes: classes, records
* Directory is count as a package. Number of packages equals number of directories.
* Preprocessor definitions between {$if xxx} and {$ifend} are removed (DefineResolver class).
* Sources imported to SonarQube are parsed through IncludeResolver class. It means, that the source will be lowercased and unknown preprocessor definitions will be cut out.

DUnit Tests
----------------------

You should put transformed DUnit xml files to directory specified using parameter `sonar.junit.reportsPath`. You can specify multiply directories separated by �,�. Then all specified directories will be parsed. The path can be either absolute or relative to the project main path.
The xml files should be renamed with �TEST-� prefix, example: �dunit.xml� -> �TEST-dunit.xml�.
I recommend you to use [dunit-extension](https://github.com/fabriciocolombo/dunit-extension) to handle these details.
