pipeline {
    agent any

    // environment {
    //     DOCKERHUB = credential
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
                    image "node:20-alpine"; reuseNode true
                }
            }
            steps{
                sh ''' 
                cd frontend
                npm ci
                npm run dev
                echo "TEST ALREADY"
                '''
            }
        }

        stage('build'){
            steps{
                sh '''
                cd frontend
                docker build -t test_image -f frontend/Dockerfile
                '''
            }
        }
    }
}