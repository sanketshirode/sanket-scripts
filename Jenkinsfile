node {

  def PULL_REQUEST = env.CHANGE_ID
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
            sh '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/maven/bin/mvn -B -DskipTests clean package'
        }

	stage('SonarQube analysis') {
            def scannerHome = tool 'Scanner';
            withSonarQubeEnv('Sonar') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=myproject-${PULL_REQUEST} -Dsonar.sources=./src -Dsonar.java.binaries=./target -Dsonar.github.pullRequest=${PULL_REQUEST} -Dsonar.github.repository=sanketshirode/sanket-scripts -Dsonar.pullrequest.provider=github -Dsonar.github.oauth=8893739de22620625c9fb6707a5d700e7381775b"
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
