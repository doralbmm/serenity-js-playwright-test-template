pipeline {
  agent { 
    docker { 
      image 'mcr.microsoft.com/playwright:v1.37.1-focal'
    }
  }
  stages {
    stage('install playwright') {
      steps {
        sh '''
          npm i -D @playwright/test
          npx playwright install
        '''
      }
    }
    stage('help') {
      steps {
        sh 'npx playwright test --help'
      }
    }
    stage('test') {
      steps {
        sh '''
          npx playwright test --list
          npx playwright test
        '''
      }
      post
      {
        always
        {
          submitJUnitTestResultsToqTest([apiKey: '03357e81-e966-4a5e-8cce-ee12d11576b8', containerID: 21724, containerType: 'release', createTestCaseForEachJUnitTestClass: false, createTestCaseForEachJUnitTestMethod: true, overwriteExistingTestSteps: true, parseTestResultsFromTestingTools: true, parseTestResultsPattern: '**.xml', projectID: 7263, qtestURL: 'https://testfly.qtestnet.com/', submitToAReleaseAsSettingFromQtest: true, submitToExistingContainer: false, utilizeTestResultsFromCITool: false])
        }
      }
    }
  }
}
