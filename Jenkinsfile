pipeline {
  agent {
    label {
      label "master"
      customWorkspace "/u01/data/jenkins/workspace/sonar_poc_GitHub/${BRANCH_NAME}"
    }
  }
  

  tools {
    maven 'maven3' 
    jdk 'JDK1.8' 
  }
  
  options { 
    disableConcurrentBuilds() 
  }
  
  stages {   
    stage('Build Project'){
      parallel{
        stage('Build Java') {
          steps {
            sh '''
              echo "PATH = ${PATH}"
              echo "M2_HOME = ${M2_HOME}"
              mvn clean install
            '''
          }
        }
      }
    }
    
	
    stage('Sonar Code Analysis') {
          steps {
            script {
              sh '''
				mvn clean verify sonar:sonar -Dsonar.login=4cdad4eb72568a6e26cf72048b54a89e79703e04
			  '''
            }

          }
        
    }
  }

}
