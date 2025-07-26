pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Clone Flask App Repo') {
            steps {
                echo '📥 Cloning your GitHub repo...'
                git url: 'https://github.com/111nawaz/Flask-app-ansible.git', branch: 'main'
            }
        }

        stage('Install Ansible (if not installed)') {
            steps {
                echo '🔧 Checking Ansible installation...'
                sh '''
                    if ! command -v ansible >/dev/null; then
                        echo "Installing Ansible..."
                        sudo apt update
                        sudo apt install -y ansible
                    else
                        echo "Ansible already installed."
                    fi
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                echo '🚀 Running Ansible Playbook...'
                sh 'ansible-playbook -i inventory.ini deploy_flask_app.yaml'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully!'
        }
        failure {
            echo '❌ Deployment failed. Check logs for errors.'
        }
    }
}

