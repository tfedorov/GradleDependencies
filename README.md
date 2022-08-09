# GradleDependencies

Project for learning gradle dependencies.

## Steps 4 installing

Step 1:</br>
From _ROOT_PROJECT_

```sh
cd BookTransitiveV1
gradle clean build publishToMavenLocal
```
Verification
```sh
ls -l ~/.m2/repository/com/tfedorov/gradledependencies/booktransitive/0.1
```
Should appear jar & pom.

Step 2:</br>
From _ROOT_PROJECT_
```sh
cd BookTransitiveV2
gradle clean build publishToMavenLocal
```
Verification
```sh
ls -l ~/.m2/repository/com/tfedorov/gradledependencies/booktransitive/0.2
```
Should appear jar & pom.

Step 2:</br>
From _ROOT_PROJECT_
```sh
cd BookTransitiveV2
gradle clean build publishToMavenLocal
```
Verification
```sh
ls -l ~/.m2/repository/com/tfedorov/gradledependencies/booktransitive/0.2
```
Should appear jar & pom.

Step 3:</br>
From _ROOT_PROJECT_

```sh
cd ScienceLibrary
gradle clean build publishToMavenLocal
```
Verification
```sh
ls -l ~/.m2/repository/com/tfedorov/gradledependencies/sciencelibrary/0.1
```
Should appear jar & pom.
