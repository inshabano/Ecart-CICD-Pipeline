pipeline {
   agent any

   tools {
      maven 'maven3'
      jdk 'jdk17'
   }

   environment {
     SCANNER_HOME=tool 'sonar-scanner'
   }
   stages {

      stage('compile') {
         steps {
            sh 'mvn clean compile'
         }
      }


      stage('test') {
         steps {
             //skipping the test cases
             sh "mvn test -DskipTests=true"
         }
      }


       stage('SonarQube Analysis') {
          steps {
             withSonarQubeEnv('sonar') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=EKART -Dsonar.projectName=EKART \
                -Dsonar.java.binaries=. '''


             }
          }
       }


   }
}