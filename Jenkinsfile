pipeline {
  agent any

  stages {
        stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later.
            }
        }

        stage('Unit Tests') {
            steps {
              sh "mvn test"
            }
        }

        stage('Docker build and push') {
            steps {
              withDockerRegistry(credentialsId: 'docker-hub', url: '') {
              sh 'printenv' // print env variables
              sh 'docker build -t serge716/numeric-app:""$GIT_COMMIT"" .'
              sh 'docker push serge716/numeric-app:""$GIT_COMMIT"" '
              }
            }
        }
    }
}
