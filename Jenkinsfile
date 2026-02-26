@Library("Shared") _

pipeline {
    agent { label 'vinod' }

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
                script {
                    clone("git@github.com:jayantkumar1604/django-notes-app.git", "dev")
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    docker_build("notes-app", "latest", "jayantkumar1604")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    // ✅ FIXED IMAGE NAME
                    docker_push("notes-app","latest","jayantkumar1604")
                }
            }
        }

        stage('Deploy') {
    steps {
        echo 'This is Deploying the code'
        sh """
            docker-compose down
            docker-compose up -d --build
        """
            }
        }
    }
}
