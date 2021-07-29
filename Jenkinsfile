pipeline {
    agent 
	  stages{
     	    stage('Code Compile'){
          steps{
	        sh 'mvn compile'
      }
	  }
	    stage('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        }
                       stage('Unit Test') {
          steps {
              sh 'mvn test'
          }
          post {
          always {
          junit allowEmptyResults: true, testResults : 'target/*.xml'
          }
          }
    }
    stage('Integration test') {
                steps {
                sh 'mvn test -Dtest=**/*IT.java'
            }
        }
	      
 stage('SonarQube Analysis') {
                    steps {
           
    		  sh 'mvn sonar:sonar \
		  -Dsonar.projectKey=vartika \
		  -Dsonar.host.url=http://3.230.147.21:9000 \
		  -Dsonar.login=9e4303cf7d09e0cfaebda01702b011989ee5501b'
            }
            }
	     	  	    stage('Deploy')
	    {
		    steps
		    {
			sh 'mvn package spring-boot:repackage'
		    }
	    }

	        stage('Backup')
	    {
		    steps{
			    sh 'mv target/sampleapp-1.0.0-SNAPSHOT-LOCAL.jar target/01.$BUILD_NUMBER.jar'
			    sh 'cp target/01.$BUILD_NUMBER.jar /opt/backup/'
			    
			    }
	    }
   }
}

{


}


}

}
