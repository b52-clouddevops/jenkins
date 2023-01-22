pipeline {
    agent any 

    stages {
        stage('One') {
            steps {
                echo "I am Stage One Step"
            }
        }

        stage('Two') {
            steps {
                echo "I am Stage Two Step"
            }
        }

        stage('Three') {
            steps {
                sh '''
                echo Hello World
                echo Hai World
                echo I am using Pipeline Syntax Generator'''
            }
        }

    }
}