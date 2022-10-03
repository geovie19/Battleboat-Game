pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "httpd"
        NEXUS_URL = "http://192.168.33.158:8081"
        NEXUS_REPOSITORY = "java-app"
        NEXUS_CREDENTIAL_ID = "NEXUS_CRED"
    }     
    					
    stages {
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/geovie19/Battleboat-Game.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                                /* `make check` returns non-zero on test failures,
                * using `true` to allow the Pipeline to continue nonetheless
                */
                sh 'make check || true' 
                junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
            }
        }
       
       stage('Deploy') {
           if(artifactExists) {
               echo :"*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
            nexusArtifactUploader(
                nexusVersion: NEXUS_VERSION,
                protocol: NEXUS_PROTOCOL,
                nexusURL: NEXUS_URL,
                groupId: pom.groupId,
                version: pom.version,
                repository: NEXUS_REPOSITORY
                credentialId: NEXUS_CREDENTIAL_ID
                artifacts: [
                    [artifactId: pom.artifactId,
                     classifier: '',
                     file : artifactPath
                     type: pom.packaging,
                     [artifactId: pom.artifactId,
                      classifier: '',
                      file:"pom.xml",
                      type: "pom"]
                ]     
                     
                
                 
              );
                    } else {
                        error "*** File: $(artifactPath}, could not be found;
                        
            steps {
                sh 'make publish'
            }
        }
    }
}
 

  
  
