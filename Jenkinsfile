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
          sh 'mvn clean package -Dsonar.login=7d97ec81447e87070bfedc6f0e450dc7c99b4bf2 -Dsonar.projectkey=amar1_key -Dsonar.organizationkey=amar1'  
        }
      }  
    }
  }  
}