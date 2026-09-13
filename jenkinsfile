pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "janhavi1608/aws-devops-flask"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    python3 -m venv test-env
                    . test-env/bin/activate
                    pip install -r app/requirements.txt
                    pytest app/test_app.py
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t $DOCKER_IMAGE:$IMAGE_TAG .
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo $DOCKER_PASSWORD | docker login -u $DOCKER_USER --password-stdin

                        docker push $DOCKER_IMAGE:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sshagent(credentials: ['kubernetes-server']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ec2-user@10.0.2.219 "
                        kubectl set image deployment/aws-devops-flask \
                        aws-devops-flask=janhavi1608/aws-devops-flask:$IMAGE_TAG
                        "
                    '''
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                sshagent(credentials: ['kubernetes-server']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ec2-user@10.0.2.219 "
                        kubectl get pods
                        "
                    '''
                }
            }
        }
    }
}
