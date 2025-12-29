pipeline {
    agent any
    stages {
        stage('Run API Tests') {
            steps {
                sh 'newman run "ReqRes.in.postman_collection.json" -e "ReqRes.postman_environment.json" -r htmlextra --reporter-htmlextra-export "reqres-newman-report.html"'
            }
        }
    }
    post {
        always {
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: true, reportDir: 'reports', reportFiles: 'report.html', reportName: 'API Test Report'])
        }
    }
}
