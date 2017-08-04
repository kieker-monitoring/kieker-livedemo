#!/usr/bin/env groovy

pipeline {
  agent {
    label 'kieker-slave-docker'
  }

  stages {
    stage('Pull Docker Base Image') {
      steps {
        sh 'docker pull openjdk:7-jre'
      }
    }
    
    stage('Build and Push Docker Container') {
      steps {
        parallel (
          'Build and Push Nightly Docker Container' : {
            sh 'docker build -t kieker/kieker-livedemo:nightly nightly/.'
            echo "Push Nightly Docker Container"
          },
          'Build and Push Release Docker Container' : {
            sh 'docker build -t kieker/kieker-livedemo:release release/.'
            echo "Push Release Docker Container" 
          }
        )
      }
    }
  }
}
