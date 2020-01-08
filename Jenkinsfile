pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }


    stages {
       stage('Build') {
           steps {
            sh 'mvn -B -DskipTests clean package'
           }
        }

	stage('SonarQube analysis') {
            steps {
                def scannerHome = tool 'Scanner'
                withSonarQubeEnv('Sonar') { // If you have configured more than one global server connection, you can specify its name
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=myproject -Dsonar.sources=./src"
                }    
            }
        }
  
    }
}
