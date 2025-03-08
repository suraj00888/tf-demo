pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY') // Replace with your Jenkins credential ID
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_KEY') // Replace with your Jenkins credential ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/RakeshRathod500/tf-demo.git' // Replace with your repo URL
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
    }

    post {
        success {
            echo 'Terraform plan executed successfully!'
        }
        failure {
            echo 'Terraform plan failed!'
        }
    }
}
