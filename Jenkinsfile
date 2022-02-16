//Declarative

 pipeline{
  agent any
   tools{
     maven "maven3.8.4"
 }
  stages{
   
     stage('git clone'){
       steps{
                           sh "echo cloning the latest application version"
                           git "https://github.com/Landmarking-tech/maven-web-app.git"
             }
  }
    stage('Build Job'){
       steps{
                           sh "echo run unittesting"
                           sh "echo unittest ok"
                           sh "mvn clean package"
                           sh "echo artifacts created"
             }
  }
    stage('Code Quality'){
        steps{
                           sh "echo running codequality report"
                           sh "mvn sonar:sonar"
             }
  }
    stage('Upload Artifact'){
        steps{
                           sh "echo upload artifacts into Nexus"
                           sh "mvn deploy"
             }
  }
     stage('Predeployment'){
        steps{ 
                            sh "docker build -t devopstestimage/newproject ."
                            sh "docker login -u devopstestimage -p Wanguni@${2074}"
                            sh "docker push devopstestimage/newproject"
             }
  }
      stage('Deployment'){
         steps{
                            sh "echo ready for deployment"
                            sh "docker run --name myproject -d -p 8000:8080 devopstestimage/newproject"
             }
   }
      stage('message'){
          steps{
                            sh "echo ci job completed"
             }
    }
  }
}
