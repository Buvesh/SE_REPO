pipeline {
    agent any

    tools {
        maven 'Maven-3.9.1'
    }

    stages {

        stage('Git Repo & Clean') {
            steps {
                // DELETE OLD GIT FOLDER
                bat 'cmd /c "if exist SE_REPO (rmdir /s /q SE_REPO) else (echo No folder to delete)"'
                // CLONE NEW CODE
                bat 'git clone https://github.com/Buvesh/SE_REPO'

                // CLEAN MAVEN PROJECT
                bat 'mvn clean -f SE_REPO/maven_java/src/pom.xml'
            }
        }

        stage('Install') {
            steps {
                bat 'mvn install -f SE_REPO/maven_java/src/pom.xml'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test -f SE_REPO/maven_java/src/pom.xml'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -f SE_REPO/maven_java/src/pom.xml'
            }
        }
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 
#SE_WEEK_9 -> PIPELINE USING SCRIPT 
