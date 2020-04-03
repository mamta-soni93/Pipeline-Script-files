pipeline {
    agent any
    stages{
       stage('checkout'){
           steps{
               git branch: "master", url: "https://github.com/mamta-soni93/SimpleMavenProject.git", credentialsId: "ce9d179a-861f-42a8-8e4e-4ec203262f9b"
           }
      }
      stage('Maven Build'){
           steps{
              sh "mvn clean install"
          }
      }
        stage('Push jar On Artifactory'){
            steps {
               script {
                 uploadArtifact()
               }
            }
          }
    }
}
def uploadArtifact() {
sh '''
        curl -sSf -H "X-JFrog-Art-Api:AKCp5ekmsgbnFTK8mAWyiHq3W9q6KuDKGwBAjvNzvT5A2Vst1j4xHSZq3oPwC8V5jmLEqz3dQ" \
       -X PUT \
       -T SimpleMavenProject.jar \
       'https://hexxa.jfrog.io/artifactory/Jenkins-integration/SimpleMavenProject.jar'
    '''
  echo "Jar file successfully deployed"
}