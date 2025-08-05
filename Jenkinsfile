@Library("Shared") _  

pipeline {
    agent { label "satya" }

    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('Code') {
            steps {
                echo 'This is cloning of code'
                script{
                    clone("https://github.com/kundaramsaisatya/django-notes-app.git","main")
                }
                echo "Code cloned successfully"
            }
        }

        stage('Build') {
            steps {
                script{
                    docker_build("notes-app","latest","ksaisatya")
                }
            }
        }

        stage('Test') {
            steps {
                echo 'This is Testing of code'
                // Add test steps if required
            }
        }

        stage('Push to Dockerhub') {
            steps {
                echo 'This is Pushing the image to docker hub'
                script{
                    docker_push("notes-app","latest","ksaisatya")
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'This is Deploying of code'
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }
    }
}
