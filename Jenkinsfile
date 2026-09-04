#!groovy
/* nif-validator
 * 20260904 Cesar Freire
 * CI-CD on project 
 */

pipeline {

  agent { 
    label 'linux' 
  }

  environment {
    HOME = "${env.WORKSPACE}"
  }

  stages {

    stage('Setup') {
      steps{
        sh 'printenv'
      }
    }


    stage('Create docker enviroment') {
      agent {
        docker {
          image: 'python:3.11-slim'
          reuseNode true
        }
      }

      steps {
        sh"""
        pip install --user -r requirements.txt
        pip install --user -r requirements-test.txt
        """
      }
    }

    stage('Unit tests') {
      agent {
        docker {
          image: 'python:3.11-slim'
          reuseNode true
        }
      }

      steps {
        sh 'python3 -m pytest --junitxml results.xml tests/'
      }

      post {
        always {
          archiveArtifacts artifacts: 'results.xml', fingerprint: true 
          junit 'results.xml'
        }
      }
    }
  }
}
