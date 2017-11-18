pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('Install') {
            steps {
                      sh "mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml"
                  }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                    step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
                }
            }
        }
        stage('deploy') {
            steps {
                sh "mvn deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"
            }
        }
    }
}