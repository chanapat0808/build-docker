pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('dockerhub')
        DOCKER_IMG = "my-test-app"
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
                docker build -t $DOCKERHUB_USR/$DOCKER_IMG .
                '''
            }
        }

        stage("push"){
            steps{
                sh '''
                echo "$DOCKERHUB_PSW" | docker login -u $DOCKERHUB_USR --password-stdin
                docker push $DOCKERHUB_USR/$DOCKER_IMG
                '''
            }
        }
    }
}