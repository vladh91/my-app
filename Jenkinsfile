pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('Install and Sonar parallel') {
            steps {
               
                        install: {
                            sh "mvn -U clean test"
                        }
            }
}
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                    
                }
            }
        }
        stage('deploy') {
            steps {
                configFileProvider([configFile(fileId: 'our_settings',variable: 'SETTINGS')])
                sh "mvn deploy -DskipTests"
            }
        }
    }
}
