pipeline{
    agent{label 'linux'}
    stages{
        stage('Checkout'){
         steps{
             git 'https://github.com/nellya27/spring-petclinic.git'
              }
        }
        stage('Build'){
            agent{docker 'maven:3.5-alpine'}
            steps{
                sh 'mvn clean package'
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                
            }
        }
        stage('Deploy'){
            steps{
               input 'Do you approve the deployment?'
               sh 'scp target/*jar ec2-user@52.208.45.208:/opt/pet'
               sh "ssh ec2-user@52.208.45.208 'nohup java -jar /opt/pet/sprint-petclinic-2.0.0.jar'" 
            }
        }
      }
   }

