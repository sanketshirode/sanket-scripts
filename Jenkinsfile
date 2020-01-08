node {
   /* agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }*/


//    stages {

	stage('SCM') {
            checkout scm
        }

       stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }

	stage('SonarQube analysis') {
            def scannerHome = tool 'Scanner';
            withSonarQubeEnv('Sonar') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=myproject -Dsonar.sources=./src"
    }
  }
 
/*
       stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
*/  
//  }
}
