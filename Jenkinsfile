pipeline {
        agent {
docker {


image 'maven:3.8.1-jdk-8'


args '-v /root/.m2:/root/.m2'


args '-v /tmp/:/tmp/'


}


}
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
                junit allowEmptyResults: true, testResults : 'target/*.xml'
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
