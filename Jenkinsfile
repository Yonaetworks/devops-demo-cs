pipeline{
    
    agent any 
    
    stages {
        
        stage('Git'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/Yonaetworks/devops-demo-cs'
                }
            }
        }
    
        stage('Pruebas unitarias'){
            steps{
                script{
                    sh '/opt/maven-3.9/bin/mvn test'
                }
            }
        }

        stage('Pruebas de integracion'){
            steps{
                script{
                    sh '/opt/maven-3.9/bin/mvn verify -DskipUnitTests'
                }
            }
        }

        stage('Build'){
            steps{
                script{
                    sh '/opt/maven-3.9/bin/mvn clean install'
                }
            }
        }

         stage('SAST-1'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube-yonaetworks') {
                        sh '/opt/maven-3.9/bin/mvn clean package sonar:sonar'
                    }
                   }  
                }
            }
        
        stage('SAST-2 Quality Gate'){
            steps{
                script{
                    waitForQualityGate abortPipeline: true, credentialsId: 'sonarqube-yonaetworks'
                }  
            }
        }

        stage('Upload Artifact'){
            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '44.202.223.9:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'demo-app-cs', version: '1.1'
                }  
            }
        }
    }  
}