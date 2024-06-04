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
            sh 'mvn compile'
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

      stage('OWASP dependency check') {
          steps {
              dependencyCheck additionalArguments: ' --scan ./', odcInstallation: 'dependency-check'
              dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
          }
       }

       stage('Build') {
          steps {
             sh "mvn package -DskipTests=true"
          }
       }
       stage('Deploy to nexus') {
          steps {
           withMaven(globalMavenSettingsConfig: 'global-maven', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
               sh "mvn deploy -DskipTests=true"
           }
          }
       }

       stage("BUILD IMAGE"){
          steps{
             script{
                withDockerRegistry(credentianlsId: 'docker-cred", toolName: 'docker') {
                        sh "docker build -t inshabano/ecart:latest -f /Dockerfile ."
                }
               
             }
          }
       }

       stage('Trivy scan') {
           steps {
                 sh "trivy image inshabano/ecart:latest >trivy-report.txt"
           }
       }

       stage('Docker push image') {
           steps {
               script{
                  withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                       sh "docker push -t inshabano/ecart:latest"
                  }
               }
           }
        }

        stage('Kubernetes deploy') {
            steps {
               withKubeConfig(caCertificate:'',clusterName:'',contextName:'',credentialsId:'k8-oken',namespace:'webspace',){
                     sh "kubectl apply -f deploymentservice.yaml -n webapps"
                     sh "kubectl get svc -n webapps"
                }
            }
         }
   }
}
