pipeline {
    agent any

    stages {
        stage('Verify Branch') {
             steps {
                echo "$GIT_BRANCH"
             }
          }
        statge("Docker Build"){
            steps {
                sh(script: 'docker image -a')
                sh(script: """
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker image -a
                    cd ..
                """)
            }
        }

    }
}
