pipeline{
  agent{ label 'Jenkins_Agent'}
  tools{
    jdk 'Java17'
    maven 'Maven3'
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
  }
}
