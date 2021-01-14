pipeline {
  agent any
    
 // tools {nodejs "node"}
    
  stages {
        
    stage('Git') {
      steps {
        git 'https://github.com/ravdy/easyio.git'
      }
    }
     
    stage('Build') {
      steps {
        sh 'rm -rf *.tar.gz'
        sh 'npm install'
         sh 'tar czf nanogram-$BUILD_NUMBER.tar.gz node_modules main.js package.json public LICENSE'
      }
    }  
    
            
    stage('Deploy') {
      steps {
        sshagent(['tomcat-user']) {
          sh 'scp ssh -o StrictHostKeyChecking=no nanogram-$BUILD_NUMBER.tar.gz -l ec2-user 13.233.37.186:/opt/'
        }
      }
    }
    stage('Create image and container') { 
      steps {
        sshagent(['node-user']) {
          script  {
            sh """ssh -tt login@host << EOF 
            cd /opt/nodejs && docker build -t node-web-app .
            docker run -p 8080:8080 -d node-web-app
            exit
            EOF"""
          }
        }
      }
    }
  }
}
