pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['apply', 'destroy'],
            description: 'Select the action to perform'
        )
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/akshaydivekar0624/eks-cluster-deployment.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init -reconfigure'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }

        stage('Terraform Action') {
            steps {
                script {
                    if (params.ACTION == 'apply') {
                        echo 'Executing Apply...'
                        sh 'terraform apply --auto-approve'
                    } else if (params.ACTION == 'destroy') {
                        echo 'Executing Destroy...'
                        sh 'terraform destroy --auto-approve'
                    } else {
                        error 'Unknown action'
                    }
                }
            }
        }
    }
}
