pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo '📥 Cloning repository...'
            }
        }

        stage('Install Ansible') {
            steps {
                echo '🔧 Installing Ansible (if not present)...'
                sh '''
                  if ! command -v ansible >/dev/null 2>&1; then
                    apt update && apt install -y ansible
                  fi
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                echo '🚀 Running Ansible playbook...'
                sh '''
                  ansible-playbook -i inventory.ini deploy_flask_app.yaml
                '''
            }
        }
    }
}
