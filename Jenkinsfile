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
                bat '''
                if not exist report mkdir report

                echo ^<html^> > report\\index.html
                echo ^<head^>^<title^>Build Report^</title^>^</head^> >> report\\index.html
                echo ^<body^> >> report\\index.html
                echo ^<h1^>Jenkins HTML Publisher Demo^</h1^> >> report\\index.html
                echo ^<p^>Build Number: %BUILD_NUMBER%^</p^> >> report\\index.html
                echo ^<p^>Status: SUCCESS^</p^> >> report\\index.html
                echo ^</body^> >> report\\index.html
                echo ^</html^> >> report\\index.html
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
