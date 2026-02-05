pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        TF_IN_AUTOMATION  = 'true'
    }

    stages {
        stage('Checkout Repo') {
            steps {
                git branch: 'main' , url: 'https://github.com/mukkamallapradeep/jenkins_terraform_kube.git'
            }
        }

        stage('Terraform Init/Plan/Apply') {
            steps {
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    sh '''
                      cd infra && \
                      terraform init && \
                      terraform plan && \
                      terraform apply -auto-approve
                    '''
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'infra/*.tf', fingerprint: true
        }
    }
}
