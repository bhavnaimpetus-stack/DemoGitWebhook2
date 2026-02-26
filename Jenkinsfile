pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Test') {
            steps {
                echo 'Running basic tests...'
                echo 'Tests passed successfully'
            }
        }
        stage('Create HTML Report') {
            steps {
                sh '''
                  mkdir -p report
                  echo "<html>
                          <head><title>Build Report</title></head>
                          <body>
                              <h1>Jenkins HTML Publisher Demo</h1>
                              <p>Build Number: ${BUILD_NUMBER}</p>
                              <p>Status: SUCCESS</p>
                          </body>
                        </html>" > report/index.html
                '''
            }
        }
    }
    post {
        success {
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'report',
                reportFiles: 'index.html',
                reportName: 'HTML Build Report'
            ])
        }
    }
}