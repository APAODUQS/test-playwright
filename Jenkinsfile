pipeline {

    agent { label 'aduquino' }

    parameters{
        string(name: 'BASE_URL', defaultValue: 'https://www.playwright.com', description: 'URL environment')
        string(name: 'TAG', defaultValue: '', description: 'Select the tag that you want to execute: @test')
    }

    environment {
        BASE_URL="${params.BASE_URL}"
        ENV = tools.git.getSimplifiedBranchName()
        BUILD = "${BUILD_NUMBER}"
    }
    
    stages {

        stage('Clean & Install Dependencies') {
            steps{
                echo "Install Dependencies"
                 sh """
                     npm cache clean --force
                     npm install
                     npx playwright install
                 """
            }       
        }

        stage('Run Tests') {
            steps{
                    echo "Run Tests"
                    sh runTests()
            }       
        }

    }
    post {
        always {
            script {
                sh "tar cfz playwright-report-${BUILD}.zip playwright-report/*"
                archiveArtifacts artifacts: "playwright-report-${BUILD}.zip", fingerprint: true
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: true, reportDir: 'playwright-report',
                reportFiles: 'index.html', reportName: "Playwright Report - ${BUILD}", reportTitles: "Playwright Report - ${BUILD}"])
                currentBuild.description = "Run tests on the ${params.RUN_PROJECT} browsers"
            }
        }               
    }         
}     

def runTests(){
    if (params.TAG == "") {
        return "npm run test"
    } else {
        return "npm run test -- --grep ${params.TAG}"
    }
}
