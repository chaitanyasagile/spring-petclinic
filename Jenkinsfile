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
        sh './mvnw pacakage'
      }  
    }
    stage('sonar') {
      steps{
        withSonarQubeEnv('Sonar_cloud') {
          sh './mvnw clean package -Dsonar.projectkey=key -Dsonar.organizationkey=suchi1'  
        }
      }  
    }
  }  
}