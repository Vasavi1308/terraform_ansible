pipeline {
    agent any

    stages {
        stage('Clone the Repo') {
            steps {
                echo 'Cloning the Code from Git'
                git branch:'main', url: 'https://github.com/nishanthkumarpathi/my-lab-infra.git'
            }
        }
        stage('Provision the Terraform Infra') {
            steps {
                echo 'Init the Terraform to Download and Apply Terraform with -auto-approve option'
                sh '''
                cd terraforminfra
                terraform init
                terraform validate
                terraform fmt
                echo "its time to apply the code"
                terraform apply -auto-approve
                '''
            }
        }
        stage('Ansible to Configure DB and Web Server') {
            steps {
                sh '''
                echo "Running Ansible Command"
                cd ansibleinfracm
                ansible-playbook playbook.yml -i inventory
                '''
            }
        }
        stage('Dummy2') {
            steps {
                echo 'Hello World'
            }
        }
    }
}