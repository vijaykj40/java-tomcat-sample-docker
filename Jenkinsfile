pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "docker build . -t vijaykj40/docker-web-app:${env.BUILD_ID}"
            }
        }

        stage('Push Docker Image to repo'){
            steps {
                sh "docker push vijaykj40/docker-web-app:${env.BUILD_ID}"
            }
        }

    }
}
