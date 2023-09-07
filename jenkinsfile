node{

echo "Jenjins home dir is:${env.JENKINS_HOME}"
echo "Job name is: ${env.JOB_NAME}"
echo "Build Number is :${env.BUILD_NUMBER}"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false], [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

def mavenHome = tool name:'maven3.9.3'

stage('CheckOutCode')
{
git branch: 'development', credentialsId: 'a935677a-cddb-4412-b537-b6124cd0c616', url: 'https://github.com/Mallidurga/maven-web-application.git'
}

stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
/*
stage('ExecuteSonarQubeReport')
{
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('UploadArtifactsInotNexus')
{
sh "${mavenHome}/bin/mvn clean  deploy"
}

stage('DeploAppIntoTomcatServer'){
sshagent(['5a073de8-c1cf-4e27-b7a9-b5edd78c441a']) {
    sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war ec2-user@172.31.11.33:/opt/apache-tomcat-9.0.78/webapps/"
}
}
*/
}
