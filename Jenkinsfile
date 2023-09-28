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
                    sh 'mvn test'
                }
            }
        }

        stage('Pruebas de integracion'){
            steps{
                script{
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }

        stage('Build'){
            steps{
                script{
                    sh 'mvn clean install'
                }
            }
        }
    }  
}