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
        sh 'mvn clean install'
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
