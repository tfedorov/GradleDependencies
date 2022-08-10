# GradleDependencies

Project for learning gradle dependencies. </br>
Please read before:

- [Gradle docs: Rich Version Constraints](https://docs.gradle.org/current/userguide/rich_versions.html#rich-version-constraints)
- [Gradle docs: Resolution Strategy](https://docs.gradle.org/current/dsl/org.gradle.api.artifacts.ResolutionStrategy.html)
- [Manage Gradle version conflicts with resolution strategy](https://proandroiddev.com/manage-gradle-version-conflicts-with-strategy-611ac3f6ce19)

Install all subprojects & finish tasks.

## Installation

Download the project and perform 5 steps described bellow.

Step 1: Transitive library v1</br>
Inside the _$ROOT_PROJECT_ folder

```sh
cd BookTransitiveV1
gradle clean build publishToMavenLocal
```

Verification for the _$HOME_ folder

```sh
% ls -l ~/.m2/repository/com/tfedorov/gradledependencies/booktransitive/0.1
total 24
-rw-r--r--  1 tfedorov  staff  2064 Aug  9 21:51 booktransitive-0.1.jar
-rw-r--r--  1 tfedorov  staff  1915 Aug  9 21:51 booktransitive-0.1.module
-rw-r--r--  1 tfedorov  staff   774 Aug  9 21:51 booktransitive-0.1.pom
```

Step 2: Transitive library v2</br>
Inside the _$ROOT_PROJECT_ folder

```sh
cd BookTransitiveV2
gradle clean build publishToMavenLocal
```

Verification for the _$HOME_ folder

```sh
% ls -l ~/.m2/repository/com/tfedorov/gradledependencies/booktransitive/0.2
total 24
-rw-r--r--  1 tfedorov  staff  2088 Aug  9 21:51 booktransitive-0.2.jar
-rw-r--r--  1 tfedorov  staff  1915 Aug  9 21:51 booktransitive-0.2.module
-rw-r--r--  1 tfedorov  staff   774 Aug  9 21:51 booktransitive-0.2.pom
```

Step 3: Library 1</br>
Inside the _$ROOT_PROJECT_ folder

```sh
cd ScienceLibrary
gradle clean build publishToMavenLocal
```

Verification for the _$HOME_ folder

```sh
% ls -l ~/.m2/repository/com/tfedorov/gradledependencies/sciencelibrary/0.1
total 24
-rw-r--r--  1 tfedorov  staff  2276 Aug  9 21:54 sciencelibrary-0.1.jar
-rw-r--r--  1 tfedorov  staff  2125 Aug  9 21:54 sciencelibrary-0.1.module
-rw-r--r--  1 tfedorov  staff  1005 Aug  9 21:54 sciencelibrary-0.1.pom
```

Step 4: Library 2</br>
Inside the _$ROOT_PROJECT_ folder

```sh
cd SoftwareLibrar
gradle clean build publishToMavenLocal
```

Verification for the _$HOME_ folder

```sh
 % ls -l ~/.m2/repository/com/tfedorov/gradledependencies/softwarelibrary/0.1
total 24
-rw-r--r--  1 tfedorov  staff  2290 Aug  9 21:55 softwarelibrary-0.1.jar
-rw-r--r--  1 tfedorov  staff  2130 Aug  9 21:55 softwarelibrary-0.1.module
-rw-r--r--  1 tfedorov  staff  1006 Aug  9 21:55 softwarelibrary-0.1.pom
```

Step 4: Client App</br>
Inside the _$ROOT_PROJECT_ folder

```sh
cd ClientApp
gradle clean build run
> Task :run
Action 1:  Take from the Science library -  -> Programming in Scala Fifth Edition 5st edition. by Martin Odersky
Action 2:  Take from the Software library -  -> Programming in Scala Fifth Edition 5st edition. by Martin Odersky
```

### Task 1

Change _build.gradle_ in _ClientApp_ and receive:

```sh
% gradle clean build run

> Task :run
Action 1:  Take from the Science library -  -> Machine Learning Yearning. by Andrew Ng
Action 2:  Take from the Software library -  -> Machine Learning Yearning. by Andrew Ng
```

Do it at 2 ways minimum.

### Task 2

Add dependency plugin and generate report for it.