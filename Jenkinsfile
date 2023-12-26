pipeline {
    agent any

    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages {
        stage('Clean WS') {
            steps {
                deleteDir()
            }
        }
    

    
        stage('Git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/murulii/youtube_app.git'
            }
        }
        
        
        stage('Sonar Server scanner') {
            steps {
                 withSonarQubeEnv('sonar_server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=youtube \
                    -Dsonar.projectKey=youtube '''
                }
            }
        }


        stage('Quality Gates') {
            steps {
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar_token' 
            }
        }






    }
}
