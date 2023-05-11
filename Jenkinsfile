node{
      
    def mavenhome = tool name: "maven3.9.1"  
     
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
    
    echo "the build number was ${env.BUILD_NUMBER}"
    stage('checkoutcode'){
        
    git branch: 'new', url: 'https://github.com/sevaorga/mvaen-web-application.git'    
        
    }
    
    
    stage('build'){

    sh "${mavenhome}/bin/mvn clean package"
        
        
        
    }
    
    
    stage('soanrscan'){
        
        
        sh "${mavenhome}/bin/mvn sonar:sonar"    
        
    }
    
    stage('deploy'){
        
        sh "${mavenhome}/bin/mvn deploy"
    }
    
    
    stage('tomacat deplaoment'){
        
        sshagent(['9ec05bc6-e5da-49a6-83f3-9091dd4b7973']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.27.167:/opt/apache-tomcat-9.0.74/webapps"
}
        
        
    }
    
    
    
    
    
    
    
}
