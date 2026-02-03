pipeline {
    agent any
    tools{
        maven 'maven'
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
    }
}