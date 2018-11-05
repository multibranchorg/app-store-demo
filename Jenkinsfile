pipeline {
  agent {
    kubernetes {
      label 'mypodtemplate-v1'
      containerTemplate {
        name 'maven'
        image 'maven:3.3.9-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
    } 
  }
  stages {
    stage('Build') {
      steps {
        sh 'echo $PATH'
        sh 'mvn clean source:jar package'
      }
    }
    stage('Browser Tests') {
      steps {
        parallel(
          "Firefox": {
            sh 'echo \'setting up selenium environment\''
            sh 'ping -c 5 localhost'
            
          },
          "Safari": {
            sh 'echo \'setting up selenium environment\''
            sh 'ping -c 8 localhost'
            
          },
          "Chrome": {
            sh 'echo \'setting up selenium environment\''
            sh 'ping -c 3 localhost'
            
          },
          "Internet Explorer": {
            sh 'echo \'setting up selenium environment\''
            sh 'ping -c 4 localhost'
            
          }
        )
      }
    }
    stage('Static Analysis') {
      steps {
        sh 'mvn findbugs:findbugs'
      }
    }
    stage('Deploy') {
      steps {
        parallel(
          "Deploy": {
            sh 'mvn source:jar package -Dmaven.test.skip'
            
          },
          "final": {
            echo 'fdsf22'
            
          }
        )
      }
    }
  }
  post {
    always {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive '**/target/*.jar'
      
    }
    
  }
}
