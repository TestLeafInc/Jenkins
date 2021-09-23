pipeline {
  agent any
  stages {
    stage('Development') {
      steps {
        echo 'This is development'
        git(url: 'https://github.com/LeafPages/EyeManage', branch: 'master')
      }
    }

    stage('Smoke Test') {
      steps {
        echo 'Smoke UI Tests'
        echo 'Smoke Tests (API)'
      }
    }

    stage('Deploy to QA') {
      steps {
        echo 'Deploy to AWS QA Server'
      }
    }

    stage('Integration Test') {
      parallel {
        stage('Integration Test (UI)') {
          steps {
            echo 'Run Full Selenium Tests'
          }
        }

        stage('Integration Test (API)') {
          steps {
            echo 'Run All API Tests'
          }
        }

        stage('Performance Testing') {
          steps {
            echo 'Run All Performance Tests'
          }
        }

      }
    }

    stage('Deploy to UAT') {
      steps {
        echo 'Deploy to UAT AWS Server'
      }
    }

    stage('Certify') {
      steps {
        echo 'Manual Certification Using Inputs'
        input(message: 'Do you like to certify?', id: 'Certify', ok: 'Yes')
      }
    }

    stage('Deploy to Prod') {
      post {
        always {
          echo 'Send Email'
        }

      }
      steps {
        echo 'Deploy to AWS Prod'
        jiraComment(issueKey: 'SFO-107', body: 'This is a comment regarding the quality of the response.')
      }
    }

  }
}
