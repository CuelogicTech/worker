pipeline { 
  agent any
  
  environment {
    NEXUS = credentials('nexus')
  }

  stages {
    stage ('Checkout Code') {
      steps {
        checkout scm
      }
    }
    stage ('Build app') {
      steps {
        sh "echo 'Add build commands here'"
      }
    }
    stage('Nexus login') {
        steps {
            sh "sudo docker login localhost:5000 -u $NEXUS_USR -p $NEXUS_PSW"
        }
    }
    stage('Docker build') {
        steps {
            sh 'env'
            sh "sudo docker build -t localhost:5000/${env.JOB_NAME}:${env.BUILD_NUMBER}.0 ."
        }
    }
    stage('Docker push') {
        steps {
            sh 'env'
            sh "sudo docker push localhost:5000/${env.JOB_NAME}:${env.BUILD_NUMBER}.0"
        }
    }
  }
}
