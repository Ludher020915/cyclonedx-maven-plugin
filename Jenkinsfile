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

    stage("Import SBOM file on the service") {
            steps {
                script {
                    sh """
                    curl --request POST \
                        --url https://de-vsm.leanix.net/services/vsm/discovery/v1/service \
                        --header 'accept: */*' \
                        --header 'content-type: multipart/form-data' \
                        --form id=LEANIX_CREDENTIALS \
                        --form sourceType=my-alerting-solution \
                        --form sourceInstance=LeanIX GmbH  \
                        --form name=my-service \
                        --form 'description=The one and only service with 110% uptime' \
                        --form "bom=@/var/lib/jenkins/workspace/Jenkinsfile-git-and-maven/target/bom.json"
                    """
                }
            }
        }
    }
}
