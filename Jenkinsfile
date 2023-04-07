pipeline {
  agent any
    
  tools {nodejs "nodejs16"}
    
  stages {
        
    stage('Git') {
      steps {
        git 'https://github.com/Debdeepghosal/bookbay.git'
      }
    }
     
    stage('Build') {
        steps {
      nodejs(nodeJSInstallationName:'nodejs16'){
        sh "npm install"
      }
    }  
    
    }      
    stage('SonarQubeReport') {
        steps {
      nodejs(nodeJSInstallationName:'nodejs16'){
        sh "npm run sonar"
      }
    }  
    
    }
    stage('UploadArtifactToNexusServer'){
      steps {
        nodejs(nodeJSInstallationName:'nodejs16'){
        sh 'npm config set registry http://44.201.142.37:8081/repository/npm-repo/ && \
        npm config set _auth YWRtaW46YWRtaW4= && \
        npm publish --registry http://44.201.142.37:8081/repository/npm-repo/'

        }
    }
    }
    stage('Run Application')
    {
      steps {
      sh 'npm install'
      sh 'pm2 start app.js'
    }

  }
}
}