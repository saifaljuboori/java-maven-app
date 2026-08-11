@Library('jenkins-shared-library') _

pipeline {
    agent any

    tools {
        maven 'my-maven'
    }

    stages {
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage("build image") {
            steps {
                script {
                    buildDockerImage('saljuboori/demo-app:jma-3.0')
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    echo "deploying the application..."
                }
            }
        }
    }
}
