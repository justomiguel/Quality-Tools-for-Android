# Quality Tools for Android

<img src="https://raw.github.com/stephanenicolas/Quality-Tools-for-Android/master/gfx/bugdroid-duke-armor.jpg" 
width="350px" />

This is an Android sample app + tests that will be used to work on various project to increase the quality of the Android platform.

The idea is that Android programming is still in its infancy compared to the Java world. 
The Android community needs more robustness in Android apps and it looks like a good idea to build on the Java world experience and use its best tools for Quality Analysis.

We want to provide a full featured industrial development environment that can be used to create more
robust projects on Android, by using any of the most interesting and popular technologies.

# Already integrated :

* Standard Android testing framework and code coverage using emma, reported in Sonar. That also covers robotium, easy mock and mockito technologies.
* Robolectric testing framework and code coverage using Cobertura, reported in Sonar.
* UI Automator testing through a new android maven plugin goal (to be released in android-maven-plugin-3.5.2) and result in sonar.
* Configuration works out of the box in eclipse
* Lint integration via Maven.
* PMD, findbugs, checkstyle integration via Maven, reported in Sonar.
* [lint android maven lint](https://github.com/lewisd32/lint-maven-plugin) integration (pom checker)
* [Spoon from square](https://github.com/square/spoon)
* [maven-android-sdk-deployer](https://github.com/mosabua/maven-android-sdk-deployer) to deliver android jars (including uiautomator)
* [sonar android lint plugin](https://github.com/jeromevdl/sonar-android-lint-plugin) 
* Testing  technologies integrated : 
    * Standard Android tests   
        * easymock
        * mockito
        * mockwebserver
        * robotium
    * robolectric tests
        * hamcrest 
        * easymock
        * mockito

# What is missing (TODO/INTEGRATE) : 

0. Using [Jacoco instead of emma](https://github.com/jacoco/jacoco/pull/64#issuecomment-12150910) would help getting more standard Sonar config 
1. get aggregated tests and code coverage 
2. get monkey through Maven, [using this technique](http://stackoverflow.com/questions/3968064/ideas-for-automating-android-monkey-runs) get the results in Sonar
3. [FEST Android](https://github.com/square/fest-android) should be included as well (thx to Jake Wharton for pointing this out).
4. Add support for Travis CI. Alternatives welcome.

# Usage

This section describes how to build & test the project using those different testing technologies.

## Install Android Latest SDK through Android SDK Manager

This can be done graphically, or [via command line (for CI servers)](http://stackoverflow.com/q/4681697/693752).

## Install the Android SDK through maven-android-sdk-deployer

As it takes time to get android jars in maven central, including android UI automator jars in maven central,
we recommend to use [maven-android-sdk-deployer](https://github.com/mosabua/maven-android-sdk-deployer) to obtain android artefacts.
This step can also be executed on a CI server.

```bash
#install Android SDK 17 local files to local maven repo  
git clone git@github.com:mosabua/maven-android-sdk-deployer.git
cd maven-android-sdk-deployer/
mvn install -P 4.2
```

## Standard Android testing APIs and code coverage using emma

To build the sample project and run the sample app on a plugged rooted device / running emulator : 

```bash
# in parent folder
mvn clean install -P emma
mvn sonar:sonar -P emma
```

you will get tests results in : target/surefire-reports/.
you will get tests coverage in : target/emma/.

Here is the result in sonar : 
<img src="https://raw.github.com/stephanenicolas/Quality-Tools-for-Android/master/gfx/screenshot-sonar-emma-config.png" width=450px/>

You may need to restart adb as root to be able to pull the emma coverage file. In a terminal, type :
```bash
adb root
```

## Robolectric and code coverage using cobertura

```bash
# in parent folder
mvn clean cobertura:cobertura -P cobertura
mvn sonar:sonar -P cobertura
```
Here is the result in sonar : 
<img src="https://raw.github.com/stephanenicolas/Quality-Tools-for-Android/master/gfx/screenshot-sonar-robolectric-config.png" width=450px/>

## UI Automator 

```bash
# in parent folder
mvn clean install -P uiautomator
mvn sonar:sonar -P uiautomator
```
Here is the result in sonar : 
<img src="https://raw.github.com/stephanenicolas/Quality-Tools-for-Android/master/gfx/screenshot-uiautomator.png" width=450px/>

## Spoon from Squareup

```bash
# in parent folder
mvn clean install -P spoon

#then browse to android-sample-tests/target/spoon-output/index.html
```

Here is the result in a browser : 
<img src="https://raw.github.com/stephanenicolas/Quality-Tools-for-Android/master/gfx/screenshot-spoon.png" width=450px/>

## Robolectric development in eclipse

To enable Robolectric development in this configuration. In eclipse, switch to maven profile "cobertura" in maven settings on the main app.

# Thanks to
 * [OCTO Technology](http://www.octo.com/en) to provide us with free time to work on that project.
 * Henri Treblay from [OCTO Technology](http://www.octo.com/en) for having ported [EasyMock](http://www.easymock.org/) to Android.
 * Thanks to [Jayway](http://www.jayway.com/blog) for their [Android Maven Plugin](http://code.google.com/p/maven-android-plugin/).
 * Thanks to [Sonar Source](http://www.sonarsource.org/) for supporting this effort, especially for this [project's configuration](https://github.com/SonarSource/sonar-examples/tree/master/projects/android).

## Quality Tools for Android in the news !!
* [Android Weekly issue #55 !] (http://androidweekly.net/#latest-issue)
* [Android Dev Weekly, issue #49 !] (http://androiddevweekly.com/2013/03/11/Issue-49.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+AndroidDevWeekly+%28%23AndroidDev+Weekly%29)
* Check us out at [Devoxx France 2013](http://www.devoxx.com/display/FR13/Tools+In+Action+Day+1) : Room Miles Davies A, Wednesday, march 27th, 5 to 5:30 pm.
