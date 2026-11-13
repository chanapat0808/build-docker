pipeline {
    agent {
        docker {
            image "node:alpine"
        }
    }

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