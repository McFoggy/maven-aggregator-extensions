# Maven aggregator with core extensions

## With polyglot core extension

Project to demo that Maven aggregator pom does not work with sub project using [polyglot](https://github.com/takari/polyglot-maven) core-extension.

````
cd polyglot
mvn validate
````

The build is failing, maven complain not to be able to find pom.xml files for sub projects.

## With jgitver

Project to demo that Maven aggregator pom does not use [jgitver](https://github.com/jgitver/jgitver-maven-plugin) core-extension in sub project ; version should be computed by [jgitver](https://github.com/jgitver/jgitver-maven-plugin).

````
cd jgitver
mvn validate
````

The build does not fail, but `prj1` version is `1.0` as it is in the pom.xml file whereas it should have been computed by jgitver.
If you go directly in the `prj1` directory and run `mvn validate`, then [jgitver](https://github.com/jgitver/jgitver-maven-plugin) corretcly computes the version.
