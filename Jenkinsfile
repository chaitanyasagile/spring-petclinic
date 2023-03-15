pipeline{
  agent{label'JDK-JDK'}
  tools {
    jdk 'JDK17'
  }
  stages{
    stage('vcs') {
      steps{
        git url: 'https://github.com/chaitanyasagile/spring-petclinic.git',
            branch: 'develop'
      }  
    }
    stage('build') {
      steps{
        sh './mvnw package'
      }  
    }
    stage('sonar') {
      steps{
        withSonarQubeEnv('sonar_cloud') {
          sh 'mvn clean sonar:sonar -Dsonar.projectkey=keyname -Dsonar.organizationkey=amar1'  
        }
      }  
    }
  }  
}