pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Checkout your Maven project from version control
        checkout scm
      }
    }

    stage('Build') {
      steps {
        // Build your Maven project
        def mvnHome = tool name: 'maven-3, type: 'maven'
        sh "${mvnHome}/bin/mvn package"
      }
    }

    stage('Generate SBOM') {
      steps {
        // Generate the SBOM file using the CycloneDX Maven plugin
        sh 'mvn org.cyclonedx:cyclonedx-maven-plugin:makeBom'
      }
    }
  }
}
