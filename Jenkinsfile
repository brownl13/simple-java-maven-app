pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
     }
   }
   stages {
    stage('Build') {
      steps {
        sh './gradlew clean build -x test'
       }
     }
     stage('Test') {
       steps {
         sh './gradlew test'
       }
       post {
         always {
           junit 'target/surefire-reports/*.xml'
         }
       }
     }
     stage('Deliver') {
       steps {
         sh './jenkins/scripts/deliver.sh'
       }
     }
    }
 }
