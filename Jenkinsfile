pipeline {
    agent any

    tools{

        nodejs 'npm'
        jdk 'jdk'
    }

    environment{
        SCANNER_HOME= tool 'sonar-scanner'
        dockeruser = "murulii"
        imagename = "youtube"
        tag = "1.0."
        imagetag = "${dockeruser}" + "/" + "${imagename}" + ":" + "${tag}" + "${BUILD_NUMBER}"
        imageandtag = "${imagename}" + ":" + "${tag}" + "${BUILD_NUMBER}"  
        
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
                  docker build --build-arg REACT_APP_RAPID_API_KEY=47e9a57e19msh039731b18bab9eep11a497jsn9684004925d0 -t $imagetag .
                  docker login -u murulii -p $dockerhub
                  docker push $imagetag
                  '''
            }
        }
        }
         


        stage('Trivy Image Scans ') {
            steps {
                sh 'trivy image $imagetag > trivyimagescanoutput.txt' 
                
            }
        }
        
        
        

        stage('Updating Yml File') {
            steps {
                dir('yml') {
                sh '''
                 cat dep.yml
                 sed -i "/${imagename}.*/${imageandtag}/"
                 cat dep.yml

                ''' 
                
            }
            }
        }



    }
}
