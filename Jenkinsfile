 // @Image(cloudbees/codeship-jenkinsfile-step:latest)          
pipeline {
  agent { docker { image "maven:3.6.3-adoptopenjdk-8" } } 
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean source:jar package'
      }
    }
    stage('Browser Tests') {
      steps {
        parallel(
          "Firefox": {
            sh 'echo \'setting up selenium environment\''
            
          },
          "Safari": {
            sh 'echo \'setting up selenium environment\''
            
          },
          "Chrome": {
            sh 'echo \'setting up selenium environment\''
            
          },
          "Internet Explorer": {
            sh 'echo \'setting up selenium environment\''
            
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
