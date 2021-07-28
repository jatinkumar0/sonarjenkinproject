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
                   sh 'mvn sonar:sonar \
                  -Dsonar.projectKey=vartika-demo \
                  -Dsonar.host.url=http://3.6.43.24:9000 \
                  -Dsonar.login=72181cfd8e803af4a94003e44d3be17630f74481'
        }
            }
         
    }
}
