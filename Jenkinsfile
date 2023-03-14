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
            tools { maven 'MAVEN' }
            steps {
                sh 'mvn package'
            }
        }
        stage('sonar analysis') {
            steps {
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=19041bf2b5a24c1b14565e850e812664a1fa5b06 -Dsonar.organization=spc-3 -Dsonar.projectKey=spc-3_bha'
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
