pipeline {
    agent any

    tools{

        nodejs 'npm'
        jdk 'jdk'
    }

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
        
        
       // stage('Sonar Server scanner') {
        //    steps {
        //         withSonarQubeEnv('sonar_server') {
          //          sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=youtube \
          //          -Dsonar.projectKey=youtube '''
          //      }
          //  }
       // }


       // stage('Quality Gates') {
          //  steps {
           //     waitForQualityGate abortPipeline: false, credentialsId: 'sonar_token' 
           // }
       // }


        stage('NPM install') {
            steps {
                sh 'npm install' 
            }
        }

       // stage('Scan file Using Trivy') {
         //   steps {
          //      sh 'trivy fs . > fsscan.txt' 
         //   }
       // }


       // stage('Depedence Check') {
        //    steps {
         //       dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
         //       dependencyCheckPublisher pattern: '**/dependency-check-report.xml' 
          //  }
      //  }

        


        stage('docker build') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
    

                sh '''
                  ls
                  docker build -t murulii/youtube:1.0.1 .
                  docker login -u murulii -p $dockerhub
                  docker push murulii/youtube:1.0.1
                  

                '''
            }
        }
        }



    }
}
