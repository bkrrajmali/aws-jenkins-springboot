pipeline {
    agent any
    stages {
        stage('Checkout From Git') {
            steps {
                git branch:'prod' , url: "https://github.com/bkrrajmali/aws-jenkins-springboot.git"
            }
        }
        stage ('Maven Validate'){
            steps {
                sh 'mvn validate'
            }
        }
        
    }
}