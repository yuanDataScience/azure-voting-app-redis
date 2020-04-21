pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            pwsh(script: 'docker images -a')
            pwsh(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """)
         }
      }
      stage('Start test app') {
         steps {
            pwsh(script: """
               docker-compose up -d
               ./scripts/test_container.ps1
            """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            pwsh(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            pwsh(script: """
               docker-compose down
            """)
         }
      }
      stage('Run Anchore') {
         steps {
            pwsh(script: """
               Write-Output "blackdentech/jenkins-course" > anchore_images
            """)
            anchore bailOnFail: false, bailOnPluginFail: false, name: 'anchore_images'
         }
      }
      stage('Run Trivy') {
         steps {
            pwsh(script: """
              C:\\Windows\\System32\\wsl.exe -- sudo trivy blackdentech/jenkins-course
            """)
         }
      }
   }
}