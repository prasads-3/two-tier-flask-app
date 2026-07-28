pipeline {
    agent any

    stages {

        stage("Code") {
            steps {
                echo "hello"
                git branch: 'master', url: 'https://github.com/prasads-3/two-tier-flask-app.git'
                echo "Code Clone ho gaya ....."
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t my-app ."
            }
        }

        stage("Test") {
            steps {
                echo "Developer / Tester testing..."
            }
        }
        stage("push to Docker Hub"){
            steps{
                  withCredentials([
            usernamePassword(
                credentialsId: 'DockerHubJack',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'
            )
        ]) {
                        
       sh '''
                echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                docker tag my-app prasad3737/two-tier-flask-app:latest
                docker push prasad3737/two-tier-flask-app:latest
            '''
                }
            }
        }
        

        stage("Deploy") {
            steps {
              sh '''
            docker compose up -d --build flask-app
        '''
            }
        }
    }
}

