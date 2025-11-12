pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mohammad-alaa-ma/iti-gp-project'
            }
        }

        stage('Initialize Terraform') {
            when {
                changeset "terraform/**"
            }
            steps {
                dir('terraform') {
                    sh 'terraform init -input=false'
                }
            }
        }

        stage('Validate Terraform') {
            when {
                changeset "terraform/**"
            }
            steps {
                dir('terraform') {
                    sh 'terraform validate'
                }
            }
        }

        stage('Plan Infrastructure') {
            when {
                changeset "terraform/**"
            }
            steps {
                dir('terraform') {
                    sh 'terraform plan -out=tfplan'
                }
            }
        }

        stage('Apply Infrastructure') {
            when {
                changeset "terraform/**"
            }
            steps {
                dir('terraform') {
                    sh 'terraform apply -auto-approve tfplan'
                }
            }
        }
    }
}
