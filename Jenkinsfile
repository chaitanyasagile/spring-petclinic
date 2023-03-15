pipeline{
  agent {label 'JDK-JDK'}
  stages{
    stage('vcs'){
      steps{
        git url: 'hhttps://github.com/chaitanyasagile/spring-petclinic.git',
            branch: 'develop'
      }
    }
    stage('build') {
      steps{
        sh './mvnw package'
      }
    }
    stage(sonar) {
      steps{
        withSonarQubeEnv('sonar_cloud') {
          sh './mvnw clean package sonar:sonar -Dsonar.organization=suchi1 -Dsonar.projectKey=teju1'
        } 
      }
    }
  }
}