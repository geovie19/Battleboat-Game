pipeline {
    agent any
    tools{
        maven 'M2_HOME'
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
           
             
            steps {
                sh 'make publish'
            }
        }
    }
}
 

  
  
