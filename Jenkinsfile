#!/usr/bin/env groovy

pipeline {
  agent {
    label 'kieker-slave-docker'
  }

  stages {
    stage('Build and Push Docker Container') {
      steps {
        parallel (
          'Build and Push Nightly Docker Container' : {
            sh 'cd nightly'
            sh 'docker build -t kieker/kieker-livedemo:nightly'
            echo "Push Nightly Docker Container"
          },
          'Build and Push Release Docker Container') {
            sh 'cd release'
            sh 'docker build -t kieker/kieker-livedemo:release'
            echo "Push Release Docker Container" 
          }
        )
      }
    }
  }
}
