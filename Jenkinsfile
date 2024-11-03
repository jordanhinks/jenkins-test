pipeline {
    // agent { 
    //     node {
    //         label 'docker-agent-python'
    //     }
    // }
    agent {
        docker {
            image "python:3.9-slim"
        }
    }

    triggers {
        pollSCM '* * * * *'
    }

    environment {
        VENV_DIR = "${WORKSPACE}/venv"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                    cd myapp
                    python3 -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                    cd myapp
                    python3 hello.py
                    python3 hello.py --name==Brad
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
}