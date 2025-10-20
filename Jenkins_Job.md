```groovy
pipeline {
    agent any

    environment {
        GIT_REPO_LINK = 'https://github.com/mahadihassanrazib/full-stack-crud-project-with-react-node-mysql.git'
        REPO_BRANCH = 'main'
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh """
                    echo 'Hello class'
                """
            }
        }
        stage("Repo Clone") {
            steps {

                echo "Project Cloning..."
                gitt url: "${GIT_REPO_LINK}",
                    branch: "${REPO_BRANCH}"

                sh "ls -lah"
            }
        }
    }
    post {
        always {
            echo 'This will always run after all the stages'
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        failure {
            echo 'The build has failed.'
        }
        success {
            echo 'The build was successful.'
        }
    }

}

```