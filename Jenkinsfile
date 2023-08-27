pipeline{
    agent any
    tools {
        jdk 'JDK'
        maven 'Maven'
    }
    environment {
        NEXUSUSER = 'admin'
        nexuspassword = 'admin'
        releaserepo = 'vpro-release'
        nexusip = '54.160.87.41'
        nexusport = '8081'
        nexuslogin = 'nexus-jenkins'
    }
    stages {
        stage ('PULL THE APPLICATION FROM GITHUB') {
            steps {
                git branch: 'master', url: 'https://github.com/Abionaraji/free-css.git'
            }
        }
        stage ('BUILD THE APPLICATION') {
            steps {
                sh 'mvn clean install' 
            }
            post {
                success{
                    echo 'New achiving'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage ('TEST') {
            steps {
                sh ' mvn test'
            }
        }
        stage ('UNIT TEST') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('INTEGRATION TEST') {
            steps {
                sh 'mvn verify -DskipUnitTest'
            }
        }
        stage ('CHECKSTYLE ANALYSIS') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('Sonarqube'){
            steps{
                withSonarQubeEnv(installationName: 'Sonarqube', credentialsId: 'sonar-jenkins') {
                    sh 'sonar:sonar'
                }
            }
        }
    }
}
