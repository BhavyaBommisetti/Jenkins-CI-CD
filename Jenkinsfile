pipeline {
    agent any
    tools {
        maven "Maven"   
    }    
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Sonar Code Analysis"){
            steps{
               withSonarQubeEnv('sonar'){
                    sh 'mvn sonar:sonar'
                    //org.codehaus.mojo:sonar-maven-plugin::sonar can alternatively used for sonar:sonar
                }
            }
        }
        stage("Artifact upload"){
          steps{
              nexusArtifactUploader artifacts: [[artifactId: 'warexample', classifier: '', file: '/var/lib/jenkins/workspace/SampleWar/target/warexample-1.0.war', type: 'war']], credentialsId: '44c0662e-9030-4882-8aa3-b804b1a41316', groupId: 'hexagon-war.com', nexusUrl: '18.224.155.110:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'devopstraining', version: '0.1'
          }
        }
     
    }
}
