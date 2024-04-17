pipeline {
  agent {
    label 'agent1'
  }

  environment {
    tag = "guyedri/flask-app:${BUILD_NUMBER}"
    replica = 5
  }

  stages {
    stage('Build App Image') {
      steps {
        dir("weather-app"){
          script {
            sh "docker build -t ${tag} ."
          }
        }
      }
    }

    stage('Push Image to Docker Hub') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
            sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
            sh "docker push ${tag}"
          }
        }
      }
    }
    stage('read&deploy') {
      steps {   
        withKubeConfig([credentialsId: 'eksToken', serverUrl: 'https://CBE7D3837922AF9EB9233DFD1B83A226.gr7.il-central-1.eks.amazonaws.com']) {
          sh 'helm upgrade --reuse-values --set weatherApp.image=$tag my-apps my-apps/'  
          sh 'helm upgrade --reuse-values --set weatherApp.replicas=$replica my-apps my-apps/'    
        }
      }
    }
  }
}