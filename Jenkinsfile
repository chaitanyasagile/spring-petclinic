pipeline{
  agent {label'JDK-JDK'}
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
         sh './mvnw clean package sonar:sonar -Dsonar.organization=suchi1 -Dsonar.projectKey=teju'
        } 
      }
    }
    stage(artifact) {
      steps{
        archiveArtifacts artifacts: '**/target/*.jar',
         fingerprint: true
      }
    }
    stage('copyingjarfile') {
      steps{
        sh 'sudo cp ${WORKSPACE}/target/spring-petclinic-3.0.0-SNAPSHOT.jar /tmp'
      }
    }
    stage('deploy') {
      steps{
        sh 'ansible-playbook -i host ansible.yml'
      }
    }
  }
}