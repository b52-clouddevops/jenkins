pipeline {
    agent any 
    
    environment {                                       // Declaring at pipeline will allow all the stages to access this variable
        ENV_URL  = "pipeline.global.com"
        SSH_CRED = credentials('SSH_CRED') 
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '3'))
        disableConcurrentBuilds()
        disableResume()
        timeout(time: 1, unit: 'MINUTES')
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    stages {
        stage('One') {
            steps {
                echo "I am Stage One Step"
                echo "ENV_URL is ${ENV_URL}"
            }
        }

        stage('Two') {
            environment {                                       // Declaring at state will allow only that stage to access that variable
                ENV_URL = "stage2.global.com"
            }
            steps {
                echo "I am Stage Two Step"
                echo "ENV_URL is ${ENV_URL}"
            }
        }

        stage('Three') {
            steps {
                sh '''
                    echo Hello World
                    echo Hai World
                    echo I am using Pipeline Syntax Generator
                    env
                '''
            }
        }
    }
}