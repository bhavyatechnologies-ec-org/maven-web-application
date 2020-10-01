  node ()
{
    def MavenHome = tool name : 'Maven3.6.3', type:'maven'
  
      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"
  
   properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')), pipelineTriggers([pollSCM('* * * * *')])])
  


/* 
properties{[
buildDiscarder(logRotator(numToKeepStr: '5')),
pipelineTriggers{[
    pollSCM('* * * * *')
]}
]}
  */  
stage('chekoutcode')
{
git branch: 'development', credentialsId: 'ff67d9b5-5051-4216-858a-e2fd24ef2903', url: 'https://github.com/bhavyatechnologies-ec-org/maven-web-application.git'
}

stage('build package')

{
    sh "${MavenHome}/bin/mvn clean package"
}    

stage ('Deployapplication')
{

deploy adapters: [tomcat8(credentialsId: '959f998b-5168-48dd-8b44-33801e0d6ce3', path: '', url: 'http://3.11.13.96:8080/')], contextPath: null, war: '**/maven-web-application.war'
}

stage ('Email')
{emailext body: 'First Pipeline project', subject: 'Pipeline Project', to: 'bhavyagowdauk@gmail.com'
}
}
