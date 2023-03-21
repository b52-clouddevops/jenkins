pipeline {
    agent any    
    parameters {
         choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Chose Environment') 
    }
    options {
        ansiColor('xterm')  // Gives colored output
    }
    stages {    
     stage('DB-n-EKS') {
        parallel {
            stage('Destroying-EKS') {
            steps {
                dir('EKS') {  git branch: 'main', url: 'https://github.com/b52-clouddevops/kubernetes.git'

                        sh ''' 
                            cd eks 
                            make destroy

                        ''' 
                     }
                 }
            }
         stage('Destroying DB') {
            steps {
              dir('DB') {
                git branch: 'main', url: 'https://github.com/b52-clouddevops/terraform-databases.git'
                sh "terrafile -f env-${ENV}/Terrafile"  
                sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                sh "terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                         }                    
                    }
                }
            }
        }
        stage('Destroying VPC') {
            steps {
              dir('VPC') {
                git branch: 'main', url: 'https://github.com/b52-clouddevops/terraform-vpc.git'
                sh "terrafile -f env-${ENV}/Terrafile"  
                sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars"
                sh "terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
              }                    
            }
        }
    }
}

