pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }
        } 

      stage('Unit Test') {
            steps {
              sh "mvn test"
            }
        }  

    stage('Docker Build and Push') {
            steps {
             withDockerRegistery([credentialsId:"docker-hub", url:""]) {
               sh 'printenv'
               sh 'docker build -t vinay8920/numeric-app:""$GIT_COMMIT"" .'
               sh 'docker push vinay8920/numeric-app:""$GIT_COMMIT""'
               
             }
           }   
        }   
    }
}
  
