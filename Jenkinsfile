pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Run API Tests') {
            steps {
                bat '''
                    if not exist reports mkdir reports
                    npx newman run "ReqRes.in.postman_collection.json" -e "ReqRes.postman_environment.json" -r cli,htmlextra --reporter-htmlextra-export "reports\\reqres-newman-report.html"
                '''
            }
        }
        
        stage('Publish Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'reports',
                    reportFiles: 'reqres-newman-report.html',
                    reportName: 'Newman HTML Report'
                ])
            }
        }
    }
    
    post {
        always {
            echo 'API tests completed'
        }
        success {
            echo 'All tests passed!'
        }
        failure {
            echo 'Some tests failed. Check the report.'
        }
    }
}