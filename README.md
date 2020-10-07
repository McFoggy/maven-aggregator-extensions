# Maven aggregator with core extensions

## With polyglot core extension

Project to demo that Maven aggregator pom does not work with sub project using [polyglot](https://github.com/takari/polyglot-maven) core-extension.

````
cd polyglot
mvn validate
````

The build is failing, maven complain not to be able to find pom.xml files for sub projects.

<details>
<summary>build error</summary>
<pre>
root@b90f3da3851b:/demo/polyglot# mvn validate
[INFO] Scanning for projects...
[ERROR] [ERROR] Some problems were encountered while processing the POMs:
[ERROR] Child module /demo/polyglot/prj1/pom.xml of /demo/polyglot/pom.xml does not exist @
[ERROR] Child module /demo/polyglot/prj2/pom.xml of /demo/polyglot/pom.xml does not exist @
 @
[ERROR] The build could not read 1 project -> [Help 1]
[ERROR]
[ERROR]   The project fr.brouillard.oss.aggregator:aggregator-polyglot:0 (/demo/polyglot/pom.xml) has 2 errors
[ERROR]     Child module /demo/polyglot/prj1/pom.xml of /demo/polyglot/pom.xml does not exist
[ERROR]     Child module /demo/polyglot/prj2/pom.xml of /demo/polyglot/pom.xml does not exist
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/ProjectBuildingException
</pre>
</details>

## With jgitver

Project to demo that Maven aggregator pom does not use [jgitver](https://github.com/jgitver/jgitver-maven-plugin) core-extension in sub project ; version should be computed by [jgitver](https://github.com/jgitver/jgitver-maven-plugin).

````
cd jgitver
mvn validate
````

The build does not fail, but `prj1` version is `1.0` as it is in the pom.xml file whereas it should have been computed by jgitver.
If you go directly in the `prj1` directory and run `mvn validate`, then [jgitver](https://github.com/jgitver/jgitver-maven-plugin) corretcly computes the version.

<details>
<summary>build result</summary>
<pre>
root@b90f3da3851b:/demo/jgitver# mvn validate
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO]
[INFO] prj1                                                               [pom]
[INFO] aggregator                                                         [pom]
[INFO]
[INFO] -----------------< fr.brouillard.oss.aggregator:prj1 >------------------
[INFO] Building prj1 1.0                                                  [1/2]
[INFO] --------------------------------[ pom ]---------------------------------
[INFO]
[INFO] ----------< fr.brouillard.oss.aggregator:aggregator-jgitver >-----------
[INFO] Building aggregator 0                                              [2/2]
[INFO] --------------------------------[ pom ]---------------------------------
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] prj1 1.0 ........................................... SUCCESS [  0.015 s]
[INFO] aggregator 0 ....................................... SUCCESS [  0.009 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.157 s
[INFO] Finished at: 2020-10-07T06:51:20Z
[INFO] ------------------------------------------------------------------------
</pre>
</details>
