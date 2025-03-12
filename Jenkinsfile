pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws_access_key') // Replace with your Jenkins credential ID
        AWS_SECRET_ACCESS_KEY = credentials('aws_secret_key') // Replace with your Jenkins credential ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/suraj00888/tf-demo.git' // Replace with your repo URL
            }
        }

        stage('Terraform Init') {
            steps {
                bat 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                bat 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                bat 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                input message: 'Do you want to apply the Terraform changes?'
                bat 'terraform apply -auto-approve tfplan'
            }
        }

        stage('Terraform Destroy') {
            steps {
                input message: 'Do you want to destroy the Terraform infrastructure?'
                bat 'terraform destroy -target=module.ec2.aws_instance.server -auto-approve'
                bat 'terraform destroy -auto-approve'
            }
        }
    }

    post {
        success {
            echo 'Terraform deployment executed successfully!'
        }
        failure {
            echo 'Terraform deployment failed!'
        }
    }
}
