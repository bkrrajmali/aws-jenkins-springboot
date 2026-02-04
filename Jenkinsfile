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
        //     stage ('Maven Validate'){
        //     steps {
        //         sh 'mvn validate'
        //     }
        // }
        // stage ('Maven Compile'){
        //     steps {
        //         sh 'mvn compile'
        //     }
        // }
        //  stage ('Maven Test'){
        //     steps {
        //         sh 'mvn test'
        //     }
        // }
        stage ('Maven Package'){
            steps {
                sh 'mvn package'
            }
          }
         }
       }
    //    stage ('Sonar Analysis') {
    //     steps {
    //         withSonarQubeEnv('sonarserver') {
    //             sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=bkrrajmali -Dsonar.projectName=SpringBootPet -Dsonar.projectKey=bkrrajmali_springbootpet -Dsonar.java.binaries=. '''
    //           }
    //        }
    //     }
    // stage('Sonar Analysis') {
    // steps {
    //     script {
    //         def scannerHome = tool 'sonar-scanner'
    //         withSonarQubeEnv('sonarserver') {
    //             sh """
    //             ${scannerHome}/bin/sonar-scanner \
    //             -Dsonar.organization=bkrrajmali \
    //             -Dsonar.projectName=SpringBootPet \
    //             -Dsonar.projectKey=bkrrajmali_springbootpet \
    //             -Dsonar.java.binaries=target
    //             """
    //                     }
    //                 }
    //             }
    //         }
    // stage("Quality Gate") {
    //         steps {
    //           timeout(time: 1, unit: 'MINUTES') {
    //             waitForQualityGate abortPipeline: true, credentialsId: 'sonar'
    //           }
    //         }
    //       }
        stage("Build Docker Image and TAG") {
            steps {
              script {
                sh 'docker build -t springboot:latest .'
              }
            }
        }
        stage("Build Docker Image and TAG") {
            steps {
              script {
                sh 'trivy image --format table --scanner vuln -o trivy-image-report.html springboot:latest'
              }
            }
        }
    }
}