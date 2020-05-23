pipeline{

  environment{
    registry = "192.168.1.252:5000/nextbox/myweb"
    dockerImage = ""
  }

  stages{
    
    stage('Checkout source'){
      steps{
        git 'https://github.com/nextbox/play-jenkins.git'
      }
    }
    stage('Build image'){
      steps{
        script{
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push image'){
      steps{
        script {
          docker.withRegistry(""){
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy app'){
      steps{
        script{
          kubernetesDeploy(configs: "myweb.yaml", kubeConfigId: "mykubeconfig")
        }
      }
    }
  }
}
