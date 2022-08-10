
node
{
    
def mavenhome= tool name: "maven3.8.6"    

stage('checkoutcode'){
    
    git credentialsId: 'a2182af5-d61b-4391-9d95-47e9ba857583', url: 'https://github.com/sevaorga/mvaen-web-application.git'
    
    
}//stage closing
    
stage('build'){
    
    
sh "${mavenhome}/bin/mvn clean package"    
    
}//stage closing

stage('soanrqube'){

sh "${mavenhome}/bin/mvn clean package sonar:sonar"    
    
    
    
}//stage closing
    
 stage('nexus'){
 sh "${mavenhome}/bin/mvn clean package sonar:sonar deploy"
 }
 
stage('tomcat'){
    
    
    sshagent(['ddcc0cfc-1b57-447f-a649-af09130b95ca']) {
    
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@43.204.231.14:/opt/apache-tomcat-9.0.65/webapps/"
    }   
    
}//stage closing
 
}//node closing
