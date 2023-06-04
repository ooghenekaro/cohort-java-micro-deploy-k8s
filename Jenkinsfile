pipeline {
    agent any 

     options {
        timeout(time: 10, unit: 'MINUTES')
     }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('karo-dockerhub')
    APP_NAME_ONE = "ooghenekaro/productcatalogue"
    APP_NAME_TWO = "ooghenekaro/shopfront"
    APP_NAME_THREE = "ooghenekaro/stockmanager"
    //IMAGE_TAG = "latest"
    //PRODUCT = "productcatalogue/Dockerfile"
    //SHOPFRONT = "shopfront/Dockerfile"
    //STOCKMANAGER = "stockmanager/Dockerfile"
    }
    stages { 
        stage('SCM Checkout') {
            steps{
           git branch: 'main', url: 'https://github.com/ooghenekaro/cohort-java-micro-deploy-k8s.git'
            }
        }

        stage('Build docker image') {
            steps {  
               sh 'docker build -t $APP_NAME_ONE -f productcatalogue/Dockerfile .'
                //sh 'docker build -t $APP_NAME_TWO -f shopfront/Dockerfile .'
                //sh 'docker build -t $APP_NAME_THREE -f stockmanager/Dockerfile .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
               // sh 'docker push $APP_NAME_ONE:$IMAGE_TAG'
                sh 'docker push $APP_NAME_TWO:$IMAGE_TAG'
                sh 'docker push $APP_NAME_THREE:$IMAGE_TAG'
            }
        }      
    }
}

