node{

def mavenHome = tool name: "maven3.8.6"

stage('checkoutcode'){

  git branch: 'development', credentialsId: 'ee8a6988-36b6-4705-9d73-0b22898774af', url: 'https://github.com/vigneshkumar2093/maven-web-application.git'
  }

stage('build'){
  
  sh "${mavenHome}/bin/mvn clean package"
  }
  
stage('ExecuteSonarQubeReport'){
  
  sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  
stage('UplodeArtifactIntoNexusRepo'){
  
  sh "${mavenHome}/bin/mvn clean deploy"
  } 
 stage ('DeploytheApplicationintoTomcat'){

  sshagent(['557d7b1b-938c-43fa-a56a-916c538bc61a']) {
  
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.223.132:/opt/apache-tomcat-9.0.70/webapps"  
   } 
  }
  
  stage('SendEmailNotifiaction') {
  
  mail bcc: 'svignesh2093@gmail.com', body: '''Build over!!

Regards,
vignesh''', cc: 'svignesh2093@gmail.com', from: '', replyTo: '', subject: 'Build over!!', to: 'svignesh2093@gmail.com'
  
  }
}//Closing bracket for node
