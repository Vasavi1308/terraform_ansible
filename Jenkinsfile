pipeline { 
    environment { 
        registry = "vasavidockerimage/python-flask-app" 
        registryCredential = 'docker_credentials' 
        dockerImage = '' 
    }
    agent any 
    stages { 
        stage('Cloning our ansible and terraform from Git') { 
            steps { 
                git branch:'master', url: 'https://github.com/Vasavi1308/terraform_ansible.git' 
            }
        }
        stage('Build the infrastructure first') {
            steps {
                sh '''cd terraformInfra
                        pwd
                        terraform init
                        pwd
                        terraform apply -auto-approve'''
            }
        } 
        stage('check if the infra is created') {
            steps {
                sh "pwd"
                sh "ansible-playbook aplaybooksapp2/ping-playbook.yml -i aplaybooksapp2/inventory"
            }
        } 
        stage('configure the created infrastructure') {
            steps {
                sh "ansible-playbook aplaybooksapp2/playbook.yml -i aplaybooksapp2/inventory"
            }
        } 
    }
}