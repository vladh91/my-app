pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('Install') {
            steps {        
                parallel(
                    install:{
                        sh "mvn -U clean test" },
                    sonar: {
                        sh "mvn sonar:sonar"
                    }
                  )
                    }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                    
                }
            }
        }
        stage('deploy') {
            steps {
                configFileProvider([configFile(fileId: 'maven_settings', variable: 'SETTINGS')]) {
                sh "mvn -s $SETTINGS deploy -DskipTests"
               }
           }
       }
    }
}
