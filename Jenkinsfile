node {
   
   stage('Code Checkout') { 
     git credentialsId: 'githubID', url: 'https://github.com/devopsprojects-2019/maven-examples.git'
     
    }
   stage('Build') {
    withMaven(jdk: 'jdk-1.8', maven: 'maven-3.6') {
      sh 'mvn clean compile'
      }
    }
   stage('Unit Test run') {
    withMaven(jdk: 'jdk-1.8', maven: 'maven-3.6') {
     sh 'mvn test'
      } 
    }
   
   withSonarQubeEnv(credentialsId: 'sonarqubeid') {
    withMaven(jdk: 'jdk-1.8', maven: 'maven-3.6') {
    sh 'mvn sonar:sonar' 
      }
    }
  stage("Quality Gate"){
          timeout(time: 10, unit: 'MINUTES') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
    }
   stage('Package to Jfrog') {
    withMaven(jdk: 'jdk-1.8', maven: 'maven-3.6') {
     sh 'mvn package'
      }
    }
   
   stage('Deploy to Dev') {
     
    }
   stage('Automation Testing') {
     
    }
   stage('Deploy to Test') {
     
    }
   stage('Smoke Testing') {
     
    }
   stage('Deploy to Prod') {
     
    }
   stage('Acceptance Testing') {
     
    }
}
