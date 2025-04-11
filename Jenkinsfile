pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
    }
    
    triggers {
        pollSCM '* * * * *'
    }
    
    environment {
        // Set up a virtual environment path, if needed
        VENV_DIR = '.venv'
    }
    
    stages {
        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python virtual environment...'
                sh '''
                    python3 -m venv $VENV_DIR
                    . $VENV_DIR/bin/activate
                    pip install --upgrade pip
                    cd python_env
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                . $VENV_DIR/bin/activate
                cd python_env
                python3 hello.py
                python3 hello.py --name=Gabi
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace'
            sh 'rm -rf $VENV_DIR'
        }
    }
}