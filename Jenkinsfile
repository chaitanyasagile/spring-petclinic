pipeline{
  agent {label 'JDK-JDK'}
  stages{
    stage('vcs'){
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
    stage(sonar) {
      steps{
        withSonarQubeEnv('sonar_cloud') {
          sh './mvnw clean package sonar:sonar -Dsonar.organization=suchi -Dsonar.projectKey=name'
        } 
      }
    }
  }
}