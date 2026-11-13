pipeline {
    agent any

    // environment {
    //     DOCKERHUB = credential
    // }

    environment {
        DOCKER_IMG = "test_img"
    }

    withCredentials([
        usernamePassword(
        credentialsId: 'dockerhub',
        usernameVariable: 'DOCKER_USERNAME',
        passwordVariable: 'DOCKER_PASSWORD')
    ])
    
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
                docker build -t $DOCKER_IMG -f frontend/Dockerfile
                '''
            }
        }
    }
}