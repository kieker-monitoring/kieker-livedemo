#!/usr/bin/env groovy

pipeline {
  agent {
    label 'kieker-slave-docker'
  }

  triggers {
    cron('44 4 * * *')
  }

  environment {
    DOCKERHUB = credentials('kiekerci-dockerhub')
    DOCKER_CONTAINER = 'kieker/livedemo'
  }
 
  stages {
    stage('Pull Docker Base Image') {
      steps {
        sh 'docker pull openjdk:7-jre'
      }
    }
   
    stage('Login at DockerHub') {
      steps {
        sh "docker login -u ${DOCKERHUB_USR} -p ${DOCKERHUB_PSW}"
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
      sh "docker logout"
      deleteDir()
    }

    success {
      sh "docker system prune -f"
    }
  }
  
}
