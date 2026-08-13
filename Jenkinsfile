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

                  sh '''
                      echo "===== POM VERSION ====="
                      grep -n "<version>" pom.xml | head -1

                      echo "===== MAVEN PROJECT VERSION ====="
                      mvn help:evaluate -Dexpression=project.version -q -DforceStdout
                  '''
             }
          }
        }

         stage("build jar") {
               steps {
                   script {
                       buildJar()

                      sh '''
                         echo "===== TARGET JARS ====="
                         ls -lh target/*.jar
                      '''
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
    }
}
