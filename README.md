Instruction to use github for Maven repository:

    app build.gradle:
     implementation 'com.omsi:lib:1.0.3'

    settings.gradle:
     maven{
            url "https://raw.githubusercontent.com/omsi-software/mvn-repo/master"
    }
             
       /*full customization:
       maven{
            url https://raw.githubusercontent.com/$organization/$repo/$branch
            credentials(AwsCredentials) {
            accessKey "someKey"
            secretKey "someSecret"
        }
     */



TO publish a module:


app build.gradle

plugins {
id 'com.android.library'
id 'kotlin-android'
id 'kotlin-kapt'
id 'maven-publish'
}

android {
...
    publishing {
        singleVariant('release') {
          //  withSourcesJar()
            //withJavadocJar()
        }
        /*multipleVariants {
            withSourcesJar()
            withJavadocJar()
            allVariants()
        }*/
    }
}

//needed dependencies
dependencies {
api 'com.omsi:lib1:1.0.1' //api will expose the dependency
}

afterEvaluate {
publishing {
publications {
release(MavenPublication) {
groupId 'com.omsi'
artifactId 'lib'
version '1.0.3'
from components.getByName('release')
}
}

        repositories {
            maven {
                name = 'myRepo' //use https-based repository server
                //url = layout.buildDirectory.dir("repo")
                url = "D:\\AndroidStudioProjects\\OMSI\\repo"
            }
        }
    }
}


THEN gradle Tasks [clean build publish]


push "com" folder to a github (gitLab?) repository
