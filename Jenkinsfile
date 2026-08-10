
pipeline {   
    agent any
    tools {
        maven 'Maven 3.9.16'
    }
    stages {
        stage("build jar") {
            steps {
                script {
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building docker image..."
                    sh 'docker build -it saljuboori/demo-app:jma-3.0 .'
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                    sh 'docker push saljuboori/demo-app:jma-3.0'

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
