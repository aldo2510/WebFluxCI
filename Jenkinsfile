
pipeline {
    // Cualquier agente
    agent {
                docker { image 'maven:3.6.3-openjdk-11-slim' }
            }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'ls -lta ./target/'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -B verify'
                sh 'ls -lta ./target/'
            }
            post{
                always{
                    //junit './target/surefire-reports/*xml'
                    junit '**/surefire-reports/*.xml'
                    
                }
                success{
                    archiveArtifacts  artifacts: '${env.WORKSPACE}/target/lab04-0.0.1-SNAPSHOT.jar', fingerprint: true
                    
                }
            }
        }
         stage('Docker') {
            steps {
                sh 'docker build --file ./src/main/docker/Dockerfile --tag demo:latest .'
                sh 'docker ps'
                 //run: docker build --file ./src/main/docker/Dockerfile --tag ${{ steps.dotenv.outputs.DOCKER_REPOSITORY}}/${{ steps.dotenv.outputs.APP}}-${{ steps.dotenv.outputs.APP_MODULE}}:latest .

            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
