pipeline {
  agent any
  environment {
    COURSE = 'DevOps'
    BRANCH = 'main'
    WWWROOT = '/var/www/html'
    SSHUSER = 'jenkins'
  }
  stages {
    stage('Audit Tools') {
      steps {
        echo "Audit all tools to be use on this pipeline ${BRANCH}"
        sh "git --version"
        sh "node --version"
        sh "npm --version"
        sh "ng --version"
        sh "ansible --version"
        echo "Devops  Folder: ${DEVOPS}"
      }
    }
    stage('Install packages') {
      steps {
        sh "git pull origin ${BRANCH}"
      }
    }
    stage('Install Front-End Packages') {
      steps {
        dir("${DEVOPS}/conduit-ui") {
          echo "Install conduit UI packages"
          sh "npm install"
        }
      }
    }
    stage('Run linting') {
      steps {
        dir("${WORKSPACE}/conduit-ui") {
          echo "npm run lint"
        }
      }
    }
    stage('Build UI') {
      steps {
        dir("${WORKSPACE}/conduit-ui") {
          sh "npm run build"
        }
      }
    }
    stage('Deploy app to ssh jenkins@ec2-35-183-57-160.ca-central-1.compute.amazonaws.com') {
      steps {
        sh "ssh jenkins@ec2-35-183-57-160.ca-central-1.compute.amazonaws.com rm -rf /home/${SSHUSER}/conduit"
        sh "scp -r ${DEVOPS} C:\Users\Administrator\Documents\Devops_PR\Devops_PR:/home/${SSHUSER}/conduit"
        sh "ssh jenkins@ec2-35-183-57-160.ca-central-1.compute.amazonaws.com sudo rm -rf ${WWWROOT}/conduit"
        sh "ssh jenkins@ec2-35-183-57-160.ca-central-1.compute.amazonaws.com sudo cp -r /home/${SSHUSER}/conduit ${WWWROOT}/conduit"
      }
    }
  }
}
