pipeline{
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
         SNAP_REPO = 'vprofile_snapshot'
         NEXUS_USER = 'admin'
         NEXUS_PASS = 'admin12345'
         RELEASE_REPO = 'vprofile_release'
         CENTRAL_REPO = 'vpro_maven_central'
         NEXUSIP = '172.31.31.126'
         NEXUSPORT = '9001'
         NEXUS_GRP_REPO = 'vpro_maven_Sgroup'
         NEXUS_LOGIN = 'nexuslogin' 
         SONARSERVER = 'sonarserver'
         SONARSCANNER = 'sonarscanner'
    }

    stages {
        stage('Build') {
            steps {
               sh 'mvn clean install -U -DskipTests -Dmaven.repo.local=~/.m2/repository'
            }       
}
    stage('UNIT TEST'){
            steps {
                sh 'mvn clean install -U -DskipTests -Dmaven.repo.local=~/.m2/repository test'
            }
        } 
        stage ('Checkstyle Analysis'){
            steps {
                sh 'mvn clean install -U -DskipTests -Dmaven.repo.local=~/.m2/repository checkstyle:checkstyle'
            }
        }
        stage('CODE ANALYSIS with SONARQUBE') {
          
		  environment {
             scannerHome = tool "${SONARSCANNER}"
          }   
}
}