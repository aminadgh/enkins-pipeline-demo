pipeline {
  agent any
  tools { 
    maven 'Maven 3.9.0' 
  }
  
  stages {
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM',
          branches: [[name: '*/main']],
          userRemoteConfigs: [[url: 'https://github.com/aminadgh/enkins-pipeline-demo.git', credentialsId: 'github-creds']]]
        )
      }
    }
    
    stage('Build') {
      steps {
        echo 'Construction...'
        sh 'mvn -B clean package -DskipTests'
      }
    }
    
    stage('Test') {
      steps {
        echo 'Tests en cours...'
        sh 'mvn test'
        junit '**/target/surefire-reports/*.xml'
      }
    }
    
    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
    
    stage('Deploy') {
      steps {
        echo 'Déploiement... (simulé)'
      }
    }
  }
  
  post {
    success { 
      echo 'Build terminé : SUCCESS' 
    }
    failure { 
      echo 'Build échoué : FAILURE' 
    }
  }
}
