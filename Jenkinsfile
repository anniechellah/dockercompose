pipeline{
    agent any
    stages{
        stage('verify tooling'){
            steps{
                sh '''
                    docker version
                    docker info
                    docker compose version
                    curl --version
                    jq --version
                    '''
            }
        }
        stage('Start Container'){
            steps{
                sh 'ddocker compose up -d --no-color --wait'
                sh 'docker compose ps'
            }
        }

        stage('Run Tests against the container'){
            steps{
                sh 'curl http://localhost:3000/param?query=demo | jq'
            }
        }
    }

    post{
        always{
            sh 'docker compose down --remove-orphans -v'
            sh 'docker compose ps'
        }
    }
}