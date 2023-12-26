pipeline {
    agent any

    tools{
        jdk 'jdk'
    }
    

    environment {

        SCANNER_HOME =tool 'sonar-scanner'
    }



    stages {
        stage('Clean WSw') {
            steps {
                deleteDir()
            }
        }
    

    
        stage('Git clones') {
            steps {
                git branch: 'main', url: 'https://github.com/murulii/youtube_app.git'
            }
        }
        
        
        stage('Sonar Server&scanner') {
            steps {
                withSonarQubeEnv('sonar_server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=youtube \
                    -Dsonar.projectKey=youtube '''
                }
            }
        }


        stage('Sonar Quality Check') {
            steps {
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar_token'
            }
        }







    }
}
