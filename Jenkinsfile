node 
{
def mavenHome=tool name: "3.9.9"
stage ('git checkout')
{
git branch: 'development', credentialsId: '371c3717-2a6e-47c5-b813-8efb0173a6ee', url: 'https://github.com/Rohit-Tadakamalla/maven-web-app-project-kk-funda.git'
}
stage ('build')
{
sh "${mavenHome}/bin/mvn clean package"
}
stage ('sonar report')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage ('nexus report')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage ('tomcat deploy')
{
    echo "deploy war using curl"
    sh """
    curl -u tomcat:tomcat \
--upload-file /var/lib/jenkins/workspace/jio-project-scripted-piplines/target/maven-web-application.war \
"http://13.232.137.213:8080/manager/text/deploy?path=/maven-web-application&update=true"
"""
}
}
