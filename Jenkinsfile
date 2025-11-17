pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages {
        stage("build jar"){
            steps{
                script {
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage("build image"){
            steps{
                script {
                    echo "building the application image..."                   
                    
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t deymow/demo-app:jma-1.1.7 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push deymow/demo-app:jma-1.1.7'

                    }
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
