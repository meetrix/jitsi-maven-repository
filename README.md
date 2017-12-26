# Jitsi Maven Repository

### Publish Android SDK as a Maven repository on github

##### 1. Get .aar from Jitsi-Meet:

    Clone and setup GitHub project for maven repository:
		    https://github.com/buddhikajay/jitsi-meet

    Run the following command within the project:
        cd android && ./gradlew assembleRelease	

    Find your .aar in this location:
		    /jitsi-meet/android/sdk/build/outputs/aar

##### 2. Customize maven repository in GitHub:

    Clone GitHub project for maven repository:
		    https://github.com/meetrix/jitsi-maven-repository

    Replace your .aar (jitsi-meet-sdk-1.9.0.aar) file of SDK into the following directory:
    (It is better if you could replace it in a separate branch of your own)
		    jitsi-maven-repository/releases/org/jitsi/react/jitsi-meet-sdk/1.9.0/

##### 3. Add repository to Android Project:

    Clone GitHub project of Android application:
		    https://github.com/meetrix/meet-android/

    Change Maven URL in build.gradle file of your project:
      https://github.com/meetrix/jitsi-maven-repository/raw/(branch_name)/releases
      Branch_name is your branch in maven repository 



Bellow is a basic script that describes the basic workflow of deploying a module
and updating the Jitsi Maven Repository.

```sh
# We use the packet-logging module as an example. Change accordingly.
MODULE_NAME=jitsi-packetlogging
MODULE_HOME=$HOME/src/jitsi/jitsi/m2/$MODULE_NAME
REPO_HOME=$HOME/src/jitsi/jitsi-maven-repository

# Deploy the module.
cd $MODULE_HOME/
mvn deploy -DaltDeploymentRepository=jmrs::default::file://$REPO_HOME/snapshots

# Update the maven repository.
cd $REPO_HOME/
git pull -r origin master
git add snapshots/
git commit -m "Updates $MODULE_NAME."
git push origin master
```
