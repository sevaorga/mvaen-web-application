
node

{
    echo "the branch name was: ${env.BUILD_NUMBER}"
 
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
 
   def mavenhome = tool name: "maven 3.8.5"
 

stage('checkoutcodegithub'){
git branch: 'development', credentialsId: '7d9a0297-2b36-44fe-981d-d6979ff0267c', url: 'https://github.com/sevaorga/mvaen-web-application.git'
}


stage('mavenbuild'){
sh "${mavenhome}/bin/mvn clean package"
}



/*stage('uploadingintonexus'){
sh "${mavenhome}/bin/mvn clean deploy"
}


stage('tomcatdeploy'){
sshagent(['e1ea57f8-5795-48c4-972a-51fb8e6d8044']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.193.243:/opt/apache-tomcat-9.0.64/webapps"   
}
}
*/


}
