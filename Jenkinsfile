pipeline {
    agent any 
    
    environment {                                       // Declaring at pipeline will allow all the stages to access this variable
        ENV_URL = "pipeline.global.com"
    }

    stages {
        stage('One') {
            steps {
                echo "I am Stage One Step"
                echo "ENv_URL is ${ENV_URL}"
            }
        }

        stage('Two') {
            environment {                                       // Declaring at state will allow only that stages to access this variable
                ENV_URL = "pipeline.global.com"
            }
            steps {
                echo "I am Stage Two Step"
            }
        }

        stage('Three') {
            steps {
                sh '''
                    echo Hello World
                    echo Hai World
                    echo I am using Pipeline Syntax Generator
                '''
            }
        }

    }
}