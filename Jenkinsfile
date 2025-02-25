pipeline {
  agent any
  
  stages {
    stage('Clone Repository') {
      steps{
        git credentialsId: 'github-credentials', url: 'https://github.com/Jeevaann/pdea.git', branch: 'main'
        }
      }
    stage('Build with Maven') {
      steps {
        sh 'mvn install package -DskipTests'
        }
      }
    stage('Build docker image'){
      steps{
        sh 'docker build -t jeevandarapu/todo-application:latest'
        }
      }
    stage('Push to docker hub'){
      steps{
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials',
        usernameVariable: 'DOCKER_USER',
        passwordVariable: 'DOCKER_PASS')]) {
        sh "echo  $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
        sh "docker push jeevandarapu/todo-application:latest"
        }
        }
        }
     stage('Deploy application'){
       steps {
         sh "docker compose up -d"
         }
         }
      stage('clean workspace'){
        steps{
        sh "rm -rf *"
        }
        }
        
       
       
       
       
       
       
       
       
