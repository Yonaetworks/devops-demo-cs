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
    }  
}