pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS_ID = 'dockerHubCredentials'
    }

    stages {
        stage('Checkout') {
            steps {
                git url:'https://github.com/SatishAero/multi_branch.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def branchName = env.BRANCH_NAME
                    def imageName = "satishvarma123/yourapp:${branchName}"
                    
                    docker.build(imageName, "-f Dockerfile .")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    def branchName = env.BRANCH_NAME
                    def containerName = "yourapp-${branchName}"
                    def imageName = "satishvarma123/yourapp:${branchName}"
                     bat "docker rm -f ${containerName} || true"
                    bat "docker run -d -p 8003:80 --name ${containerName} ${imageName}"
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
