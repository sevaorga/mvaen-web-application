pipeline{
      agent any
      tools{
      
      maven "maven3.9.1"
      }

    
    
  

      
        
      stages{        
    stage('checkoutcode'){
          steps{     
         notifyBuild('STARTED')
    git branch: 'new', url: 'https://github.com/sevaorga/mvaen-web-application.git'    
        
    }
    }
    
    stage('build'){

          steps{
          sh "mvn clean package"
        
          }
        
    }
    
    
    stage('soanrscan'){
        
          steps{
        sh "mvn sonar:sonar"    
        
    }
    }
    stage('deploy'){
          steps{   
        sh "mvn deploy"
    }
    
    }
    stage('tomacat deplaoment'){
          steps{   
        sshagent(['9ec05bc6-e5da-49a6-83f3-9091dd4b7973']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.27.167:/opt/apache-tomcat-9.0.74/webapps"
}
        
          }
    }
     
    
    
      
    
    
      
      
      }
      post {
  
  aborted {
  
  
   notifyBuild("currentBuild.result")
  
  }
  success {
  
  notifyBuild("currentBuild.result")
   
  }
  unsuccessful {
  notifyBuild("currentBuild.result")
  
    
}


}//pipeline closing





def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}




