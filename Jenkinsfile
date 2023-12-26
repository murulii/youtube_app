pipeline {
    agent any




    stages {
        stage('Clean WS') {
            steps {
                deleteDir()
            }
        }
    }

    stages {
        stage('Git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/murulii/youtube_app.git'
            }
        }
    }
}
