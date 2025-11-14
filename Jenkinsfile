CODE_CHANGES == getGitChanges()
pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')
    }
    tools {
        maven 'maven-3.9'
    }
    parameters {
        string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod')
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage("build"){
            steps {
                echo 'building the application'
                echo "building version ${NEW_VERSION}"  //wants it ot be interpreted as a string variable that is passed
                echo 'building version ${NEW_VERSION}'  //want it to appear literally as the way it is
                sh "mvn install"
            }
        }
        stage("test"){
            when {
                expression {
                    params.executeTests == true
                    params.executeTests
                }
            }
            steps {
                echo 'testing the application'
            }
        }
        stage("deploy"){
            steps {
                echo 'deploying the application'
                echo "deploying version ${params.VERSION}"
                withCredentials([
                    usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD) {
                        sh "some script ${USER} ${PWD}"
                    }
                ])
            }
        }
  }
}
