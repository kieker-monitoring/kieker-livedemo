#!/usr/bin/env groovy

pipeline {
  agent {
    label 'kieker-slave-docker'
  }

  environment {
    DOCKERHUB = credentials('kiekerci-dockerhub')
    DOCKER_CONTAINER = 'kieker/kieker-livedemo'
    DOCKERHUB_REGISTRY = 'https://registry.hub.docker.com'
  }
 
  stages {
    stage('Pull Docker Base Image') {
      steps {
        sh 'docker pull openjdk:7-jre'
      }
    }
   
    stage('Login at DockerHub') {
      steps {
          echo "Pre-login"
          sh "docker login -u ${DOCKERHUB_USR} -p ${DOCKERHUB_PSW} ${DOCKERHUB_REGISTRY}"
          echo "Post-login"
      }
    }
 
    stage('Build and Push Docker Container') {
      steps {
        parallel (
          'Build and Push Nightly Docker Container' : {
            sh "docker build -t ${DOCKER_CONTAINER}:nightly nightly/."
            sh "docker push ${DOCKER_CONTAINER}:nightly"
          },
          'Build and Push Release Docker Container' : {
            sh "docker build -t ${DOCKER_CONTAINER}:release release/."
            sh "docker push ${DOCKER_CONTAINER}:release"
          }
        )
      }
    }
  } 
 
   post {
    always {
      sh "docker logout ${DOCKERHUB_REGISTRY}"
    }
  }
  
}
