pipeline{
  agent{ label 'Jenkins_Agent'}
  tools{
    jdk 'Java17'
    maven 'Maven3'
  }
  environment{
    APP_NAME = "register-app-pipeline"
    RELEASE = "1.0"
    DOCKER_USER = "ronorozoro"
    DOCKER_PASS = 'dockerhub'
    IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
    IMAGE_TAG = "${RELEASE}- ${Build_NUMBER}"
  }
  stages{
    stage( "Cleanup Workspace"){
      steps{
        cleanWs()
      }
    }
    stage("checkout from SCM"){
      steps{
        git branch: 'main' , credentialsId: 'github' , url: 'https://github.com/anandtpradeep/register-app'
      }
    }
    stage("build application"){
      steps{
        sh "mvn clean package"
      }
    }
    stage("test application"){
      steps{
        sh "mvn test"
      }
    }
    stage("build and push a docker image"){
      steps{
        script{
          docker.withRegistry('',DOCKER_PASS){
            docker_image = docker.build "${IMAGE_NAME}"
          }
          docker.withRegistry('',DOCKER_PASS){
              docker_image.push("${IMAGE_TAG}")
              docker_image.push("latest")}
          
          }
          
          }
        }
      }
    
  }
