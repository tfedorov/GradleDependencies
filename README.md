# GradleDependencies

This project for learning Gradle dependencies management task. </br>
[Install & configure](#Installation) projects modules & solve [tasks](#tasks).

Please read before:
* Gradle docs
  * [Working with Dependencies: Learning the basics](https://docs.gradle.org/current/userguide/core_dependency_management.html)
  * [ Working with Dependencies: Controlling Transitives](https://docs.gradle.org/current/userguide/dependency_constraints.html)
* [Manage Gradle version conflicts with resolution strategy](https://proandroiddev.com/manage-gradle-version-conflicts-with-strategy-611ac3f6ce19)

### Description of project modules 
The project consist all required modules for the task. You need to compile them and publish to Your local repository (_publishToMavenLocal_ command).

The project has runnable [module _ClientApp_](../main/ClientApp).<br/>
_ClientApp_ has 2 dependency libraries: [_ScienceLibrary_](../main/ScienceLibrary) and ['_SoftwareLibrary_'](../main/SoftwareLibrary).<br/>
Both libraries have a dependency on the '_Book_' module (but on different version).<br/>
_ScienceLibrary_ depends on [_booktransitive:0.1_](../main/BookTransitiveV1), _SoftwareLibrary_ on - [_booktransitive:0.2_](../main/BookTransitiveV2).<br>

Gradle [__dependency management__](https://docs.gradle.org/current/userguide/core_dependency_management.html) resolves version of the _Book_ the _ClientApp_ will use.<p/>

Resolve dependencies by changing [build.gradle](../main/ClientApp/build.gradle) file.

## Tasks
### Task 1 - preparation
* [Install & configure](#Installation) projects
* Run the command bellow, check results:
```sh
% gradle clean build run

> Task :run

 ...
    |  /                                           /.
    \_/___________________________________________/.

Action 1: I take from the 'Science Library'   a book 'Programming in Scala Fifth Edition 5st edition.' by Martin Odersky (v2)
Action 2: I take from the 'Software Library'  a book 'Programming in Scala Fifth Edition 5st edition.' by Martin Odersky (v2)

The application is over...

```
* Print dependencies tree, and explain it.

### Task 2 - dependency management

Change resolved _Book_ dependencies for this task. The result should be:
```sh
% gradle clean build run

> Task :run

 ...
    |  /                                           /.
    \_/___________________________________________/.

Action 1: I take from the 'Science Library'   a book 'Machine Learning Yearning'. by Andrew Ng. (v1)
Action 2: I take from the 'Software Library'  a book 'Machine Learning Yearning'. by Andrew Ng. (v1)


The application is over...

```

Do it by changing [build.gradle](../main/ClientApp/build.gradle) file.
Provide several way to do that:
* Declaring simple version declaration
* Declaring rich versions
* Exclude unnecessary dependency
* Use resolution strategy

Explain what each method does. Show pros/contra of each of them.

### Task 3 - optional

* Add code for failing on versions conflict.
* Add code for failing on specific _Book_ version.
* Do randomly _Book_ resolving on each build. Make no sense in prod, but useful for understanding internal process.
* Use api scope in submodules.
* Find/use Gradle plugin for dependencies management.

## Installation

You should have a JVM v > 9, Scala v > 13 (Or You may configure lower version)

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

    ____________________________________________
 / \                                            \.
|   |                                           |.
 \_ |                                           |.
    |   This is a tutorial application for the  |.
    | Gradle Dependencies managment.            |.
    |                                           |.
    | The App performs 2 actions:               |.
    |  - take a 'Book' in a 'Science Library'   |.
    |  - take a 'Book' in a 'Software Library'  |.
    |                                           |.
    |  'Science Library' and 'Software Library' |.
    | are 2 modules each of them contains       |.
    | a 'Book' module as a dependency           |.
    |                                           |.
    |  There are several versions of a 'Book':  |.
    |   - booktransitive:0.1                    |.
    |   - booktransitive:0.2                    |.
    |                                           |.
    |  The Gradle defines version of the 'Book' |.
    | by DEPENDECY MANAGEMENT.                  |.
    |                                           |.
    |   ________________________________________|___
    |  /                                           /.
    \_/___________________________________________/.

Action 1: I take from the 'Science Library'   a book 'Programming in Scala Fifth Edition 5st edition.' by Martin Odersky (v2)
Action 2: I take from the 'Software Library'  a book 'Programming in Scala Fifth Edition 5st edition.' by Martin Odersky (v2)

The application is over...
```
