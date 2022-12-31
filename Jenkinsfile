//Jenkins pipeline script
//Groovy script 

node{
  def mavenHome = tool name: 'maven3.8.6'
  stage('CodeClone') {
    git "https://github.com/atehrene/maven-web-apps"
  }
  stage('mavenBuild') {
    sh "${mavenHome}/bin/mvn clean package"
  }

  stage('CodeQuality') {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  // execute the CodeQuality report with sonar
  }
  stage('emailQualityIssues') {
    emailext body: '''Thanks

Landmark Technologies''', recipientProviders: [developers()], subject: 'status of build', to: 'mylandmarktech@gmail.com'
  }

   stage('UploadNexus') {
    sh "${mavenHome}/bin/mvn deploy"
    //mvn deploy  are uploaded in to nexus
  }

  stage('DeployTomcat') {
  deploy adapters: [tomcat9(credentialsId: '0363b789-e10c-4bae-9217-cfc1d774703a', path: '', url: 'http://18.216.237.184:8080')], contextPath: null, war: '**/*.war'
  }
  stage('emailDeployIssues') {
    emailext body: '''Thanks

Landmark Technologies''', recipientProviders: [developers()], subject: 'status of build', to: 'mylandmarktech@gmail.com'
  }
 
}

