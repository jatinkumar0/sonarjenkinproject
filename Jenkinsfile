pipeline {
        agent any
        stages {
            stage('compile') {
                steps {
                       sh 'mvn compile'
            }
        }
            stage('Build') {
                steps {
                      sh 'mvn clean install'
            }
        }
                        stage('test') {
                                steps {
                                       sh 'mvn test'
                        }
                    post {
                    always {
                        junit 'target/*.xml'
                        }
                }
         }
            stage('Integration testing') {
                steps {
                      sh 'mvn test -Dtest=**/*IT.java'
            }
        }
            stage('sonarqube integration') {
                steps {
                    withSonarQubeEnv(credentialsId: 'sonar', installationName: 'sonar'){
                        sh 'java -jar jacococli.jar report target/jacoco.exec --classfiles target/  --xml target/report.xml'
                       sh 'mvn sonar:sonar \
                                                           -Dsonar.tests=src/test/ \
                                                   -Dsonar.junit.reportsPath=target/ \
                                               -Dsonar.coverage.jacoco.xmlReportPaths=target/report.xml'
            }
        }
            }
            stage('Package')
                             {
                                steps
                                     {
                                       sh 'mvn package spring-boot:repackage'
                                     }
                         }
            stage('renaming the jar') {
                steps {
                      sh 'mkdir -p /opt/backup'
                      sh 'mv target/sampleapp-1.0.0-SNAPSHOT-LOCAL.jar target/java-jar.${BUILD_NUMBER}.jar'
            }
        }
            stage('backing up the jar') {
                steps {
                      sh 'cp target/java-jar.${BUILD_NUMBER}.jar /opt/backup/'
            }
        }
    }
}
