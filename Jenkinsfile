pipeline{
agent any 

stages{

stage('clean and build'){
steps{
       sh 'mvn clean'
       sh 'mvn -Dmaven.test.failure.ignore=true install'
}

}

stage("SonarQube analysis") {
       
            steps {
              withSonarQubeEnv('sonarqube') {
                sh 'mvn sonar:sonar'
              }
            }
          }
   stage('Nexus Artifact Upload') {
          steps{
     nexusArtifactUploader artifacts: [[artifactId: 'test', classifier: '', file: '/var/lib/jenkins/.m2/repository/koddas/web/war/wwp/1.0.0/wwp-1.0.0.war', type: 'war']], credentialsId: 'trainee', groupId: 'falcons.devops', nexusUrl: 'ec2-18-224-155-110.us-east-2.compute.amazonaws.com:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'devopstraining', version: '0.0.1'
          }}
       stage('DEPLOY'){
              steps{
              
              deploy adapters: [tomcat8(credentialsId: '839a7add-99f1-4291-9d6b-92b0be6c6c06', path: '', url: 'http://3.18.109.31:8090')], contextPath: 'web', onFailure: false, war: '**/*.war'
              }
       
       }

}
}
