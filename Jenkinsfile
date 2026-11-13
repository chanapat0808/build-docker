pipeline {
    agent any


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
                docker build -t test_image .
                '''
            }
        }
    }
}