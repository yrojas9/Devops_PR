pipeline {
  agent any
  stages {
    stage('Hello World') {
      steps {
        echo "Audit all tools to be used on this pipeline ${BRANCH}"
        sh "git --version"
        sh "node --version"
        sh"npm --version"
        sh "git --version"
        sh "ng --version"
        sh "ansible --version"
      }
    }

  }
  environment {
    Course = 'devopscalgary'
    BRANCH = 'main'
  }
}