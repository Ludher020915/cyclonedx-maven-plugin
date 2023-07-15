pipeline{
  stages{
    // your build here
    
    stage("Generate SBOM with CycloneDX maven  plugin"){
       sh "mvn org.cyclonedx:cyclonedx-maven-plugin:makeBom"
    }
  }
}
