node
{
   properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '6')), pipelineTriggers([githubPush()])])
       def mavenhome = tool name: "maven 3.6.3"
    stage('git')
    {
        git branch: 'develop', credentialsId: 'b4931b28-7b90-4c8a-8ccc-135725dd32b7', url: 'https://github.com/kss-760/flipkart.git'
    }
    stage('build')
    {
        sh "$mavenhome/bin/mvn clean package"
    }
 
    stage('sonarqube')
    {
        sh "$mavenhome/bin/mvn sonar:sonar"
    }
    stage('nexus')
    {
        sh "$mavenhome/bin/mvn deploy"
    }
   /*
    stage('deploytomcat')
    {
        sshagent(['a48409b5-bda8-40d5-a6fb-a7acd69ba9a0']) 
        {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.248.115:/opt/apache-tomcat-9.0.31/webapps/"
}
    }
    stage('emailnotification')
    {
        emailext body: '''hi guys this is the build status

Regards,
Kishore.''', subject: 'build status', to: 'kishoreyuva50@gmail.com,kishoreyuva760@gmail.com,kishoreyuva6049@gmail.com'
    } */
   }
