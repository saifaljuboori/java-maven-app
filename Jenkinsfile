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

        stage("build and push image") {
            steps {
                script {
                    buildDockerImage('saljuboori/demo-app:jma-4.2')
                    dockerLogin()
                    dockerPush('saljuboori/demo-app:jma-4.2')
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
