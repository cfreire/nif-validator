#!groovy
/* nif-validator
 * 20260904 Cesar Freire
 * CI-CD on project 
 */

pipeline {
  agent { 
    label: "linux" 
  }
  environment {
    HOME = "${env.WORKSPACE}"
  }

  stages {
    stage('Setup') {
      steps{
        sh printenv
      }
    }
  }
}
