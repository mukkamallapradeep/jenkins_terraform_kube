pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
        AWS_DEFAULT_REGION    = "ap-south-1"
    }

    stages {
        stage('Checkout Repo') {
            steps {
                git 'https://github.com/mukkamallapradeep/jenkins_terraform_kube.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'cd infra && terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'cd infra && terraform plan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'cd infra && terraform apply -auto-approve'
            }
        }
    }
}
