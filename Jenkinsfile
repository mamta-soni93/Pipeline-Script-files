pipeline {
    agent any
	tools {
        maven 'maven-3.6.0'
    }
    stages{
       stage('checkout'){
           steps{
               git branch: "master", url: "https://github.com/mamta-soni93/SimpleMavenProject.git", credentialsId: "ce9d179a-861f-42a8-8e4e-4ec203262f9b"
           }
      }
      stage('Maven Build'){
		   tools {
                   jdk "JAVA_HOME"
                }
			steps {
                    bat 'java -version'
					bat "mvn clean install"
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
bat '''
        curl -sSf -H "X-JFrog-Art-Api:AKCp5ekmsgbnFTK8mAWyiHq3W9q6KuDKGwBAjvNzvT5A2Vst1j4xHSZq3oPwC8V5jmLEqz3dQ" \
       -X PUT \
       --form files=@"target/jb-hello-world-maven-0.1.0.jar" \
       "https://hexxa.jfrog.io/artifactory/Jenkins-integration/jb-hello-world-maven-0.1.0.jar"
    '''
  echo "done"
}

