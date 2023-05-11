pipeline{
      agent any
      tools{
      
      maven "maven3.9.1"
      }

    
    
    
      
        
      stages{        
    stage('checkoutcode'){
          steps{     
        
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
      

}//pipeline closing









