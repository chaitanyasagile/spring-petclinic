pipeline {
    agent { label 'Master' }
	triggers { pollSCM ('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Bharatkumar5690/spring-petclinic.git',
                    branch: 'developer'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('sonar analysis') {
            steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=ea06c1ce5d1ee81e35db29d8cb0de69b42c70278 -Dsonar.organization=springpetclinic-2 -Dsonar.projectKey=springpetclinic-2_bharat'
                }
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}
