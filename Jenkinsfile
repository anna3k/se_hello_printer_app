pipeline {
    agent any
    stages {
        stage('Deps') {
            steps {
	            sh 'make deps'
        	}
        }
        stage('Lint') {
            steps {
	            sh 'make lint'
        	}
        }
        stage('Test') {
            steps {
	            sh 'make test_xunit || true'
              step([$class: 'XUnitBuilder',
                thresholds: [
                  [$class: 'SkippedTreshold', failureTheshold: '0'],
                  [$class: 'FailedTreshold', failureTheshold: '1']
                ]
                tools: [[$class: 'JUnitType', pattern: 'test_results.xml']]])
          }
        }
    }
}
