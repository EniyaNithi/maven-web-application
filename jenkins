node  {
echo "Job name is: ${env.JOB_NAME}"
echo "Node name is: ${env.NODE_NAME}"
def mavenHome = tool name: 'maven-3.8.4'
stage('checkout code') {
git branch: 'development', credentialsId: '4ecabf9c-054d-4fae-86dc-ff30e9c5b22a', url: 'https://github.com/EniyaNithi/maven-web-application.git'
}
stage('Build') {
 sh "${mavenHome}/bin/mvn clean package"
}
stage('ExcuteSonarQubeReport') {
 sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('uploadArtifactsintoNexus') {
 sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployApplicationIntoTomcatSerrver'){
sshagent(['a44734a3-8aa6-43c9-ab60-674572affc0b']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.131.26:/opt/apache-tomcat-9.0.62/webapps/"

}
}
}
