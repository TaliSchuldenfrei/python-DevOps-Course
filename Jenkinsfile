
pipeline{
    agent any
    stages{
        stage("Checkout Code"){
            steps{
                git branch: 'main', url:'https://github.com/TaliSchuldenfrei/python-DevOps-Course.git'
            }
        }
        
        stage("Docker Build+Tag"){
            steps{
                sh 'docker build -t taliai/python-demo:1.0.3 .'
            }
        }
        
        stage("Docker Push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push taliai/python-demo:1.0.3
                    '''
                    
                }
            }
        }
        
        stage("Docker Run"){
            steps{
                sh 'docker run taliai/python-demo:1.0.3'
            }
        }
    }
}
