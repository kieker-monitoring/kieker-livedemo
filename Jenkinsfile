#!/usr/bin/env groovy

pipeline {
  agent {
    label 'kieker-slave-docker'
  }

  stages {
    stage('Build and Push Docker Container') {
      parallel {
        stage('Build and Push Nightly Docker Container') {
          steps {
            sh 'cd nightly'
            sh 'docker build -t kieker/kieker-livedemo:nightly'
            echo "Push Nightly Docker Container"
          }
        }
        stage('Build and Push Release Docker Container') {
          steps {
            sh 'cd release'
            sh 'docker build -t kieker/kieker-livedemo:release'
            echo "Push Release Docker Container" 
          }
	}
      }
    }
  }
}
