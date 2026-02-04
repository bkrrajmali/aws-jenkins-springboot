pipeline {
    agent any
    tools{
        maven 'maven'
        sonarQubeScanner 'sonar-scanner'
    }
    stages {
        stage('Checkout From Git') {
            steps {
                git branch:'prod' , url: "https://github.com/bkrrajmali/aws-jenkins-springboot.git"
            }
        }
        stage ('Maven Parallel Stages') {
            parallel {
            stage ('Maven Validate'){
            steps {
                sh 'mvn validate'
            }
        }
        stage ('Maven Compile'){
            steps {
                sh 'mvn compile'
            }
        }
         stage ('Maven Test'){
            steps {
                sh 'mvn test'
            }
        }
        stage ('Maven Package'){
            steps {
                sh 'mvn package'
            }
          }
         }
       }
       stage ('Sonar Analysis') {
        steps {
            withSonarQubeEnv('sonar-server') {
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=SpringBootPet -Dsonar.projectKey=bkrrajmali_springbootpet \
                        -Dsonar.java.binaries=. '''
              }
           }
        }
    }
}