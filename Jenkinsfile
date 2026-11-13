pipeline {
    agent any

    environment {
        DOCKER_IMG = "my-test-app"
        DOCKERHUB = credentials('dockerhub')
    }


    // environment {
        
    // }
    // withCredentials([
    //     usernamePassword(
    //     credentialsId: 'dockerhub',
    //     usernameVariable: 'DOCKER_USERNAME',
    //     passwordVariable: 'DOCKER_PASSWORD')
    // ])

        
    
    stages{
        stage('test'){
            agent {
                docker {
                    image "node:22-alpine"; reuseNode true
                }
            }
            steps{
                sh ''' 
                cd frontend
                npm ci
                npm run test
                echo "TEST ALREADY"
                '''
            }
        }

        stage('build'){
            steps{
                sh '''
                cd frontend
                docker build -t $DOCKER_IMG .
                '''
            }
        }

        stage("push"){
            steps{
                sh '''
                echo "$DOCKER_PASSWORD" | docker login -u $DOCKER_USERNAME --password-stdin
                docker push $DOCKER_IMG:latest
                '''
            }
        }
    }
}