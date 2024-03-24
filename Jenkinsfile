pipeline{
   agent any

   tools {
      maven 'maven3'
      jdk 'jdk17'
   }

   environment{
     SCANNER_HOME = tool 'sonar-scanner'
   }
   stages{
      stage('git checkout'){
         steps{
             git branch: 'main', url: 'https://github.com/inshabano/Ecart-CICD-Pipeline.git'
         }
      }


      stage('compile'){
         steps{
            sh 'mvn clean compile'
         }
      }


      stage('test'){
         steps{
             sh 'mvn test -DskipTests=true'              //skipping the test cases
         }
      }


       stage('SonarQube Analysis'){
          steps{
             withSonarQubeEnv('sonar') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=EKART -Dsonar.projectName=EKART \
                -Dsonar.java.binaries=. '''


             }
          }
       }


   }
}