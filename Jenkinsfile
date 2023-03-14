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
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.login=ca4cb5e18e327e8530dc1a982971314c02328665 -Dsonar.organization=spc-3 -Dsonar.projectKey=spc-3_bharat'
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
