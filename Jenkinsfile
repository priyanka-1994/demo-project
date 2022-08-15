pipeline{
  agent any
  stages{
    stage('git'){
      steps{
        git url:'https://github.com/priyanka-1994/demo-project.git'
    }
  }
    stage("Build Image"){
      steps{
        script{
          myapp = docke.build("prikale/html-web:${env.BUILD_ID}")
        }
      }
    }
    stage("push image"){
      steps{
        script{
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            myapp.push("latest")
            myapp.push("${env.BUILD_ID}")
          }
        }
      }
    }
    stage("deploy app on k8s"){
      steps{
        script{
           kubernetesDeploy(configs: "html-web.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }
  }
}
