@Library('jenkins-shared-library') _

pipeline {
    agent any

    tools {
        maven 'my-maven'
    }

    stages {
        stage("increment version") {
           steps {
              script {
                  incrementVersion()
             }
          }
        }

         stage("build jar") {
               steps {
                   script {
                       buildJar()
                  }
               }
         }

        stage("build and push docker image") {
            steps {
                script {
                    def version = getVersion()

                    env.IMAGE_NAME = "saljuboori/demo-app:${version}"

                    echo "Docker image: ${env.IMAGE_NAME}"
                    buildDockerImage(env.IMAGE_NAME)
                    dockerLogin()
                    dockerPush(env.IMAGE_NAME)
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
        stage("commit version") {
            steps {
                script {
                    commitVersion()
               }
            }
        }
    }
}
