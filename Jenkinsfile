pipeline {
    agent any

    environment {
        INVENTORY = 'inventory.ini'
        INSTALL_PLAYBOOK = 'install_docker.yml'
        DEPLOY_PLAYBOOK = 'deploy_app.yml'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/rutika612/php-devops-project.git'
            }
        }

        stage('Install Docker') {
            steps {
                sh "ansible-playbook -i $INVENTORY $INSTALL_PLAYBOOK"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myphpapp .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:80 myphpapp'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                sh "ansible-playbook -i $INVENTORY $DEPLOY_PLAYBOOK"
            }
        }
    }
}
