pipeline {
  agent any
  tools{
    maven 'M2_HOME' 
  stages {
    stage('checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/geovie19/Battleboat-Game.git'
      }
  }
    stage('code build'){
      steps{
        sh 'mvn clean package'
    }
  } 
    stage('Test') {
            steps {
             sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

}  
  
  
