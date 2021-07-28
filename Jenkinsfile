pipeline {

agent any {tools }

stages{

stage()  pipeline {
    agent {
        docker {
            image 'maven:3.8.1-jdk-8'
            args '-v /root/.m2:/root/.m2'
	          args '-v /opt/:/opt/'
        }
    }
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
           withSonarQubeEnv(credentialsId: "sonar", installationName: "sonar")
        {  
        sh 'java -jar jacococli.jar report target/jacoco.exec --classfiles target/  --xml target/report.xml'
           sh 'mvn sonar:sonar \
                    -Dsonar.tests=src/test/ \
           -Dsonar.junit.reportsPath=target/ \
            -Dsonar.coverage.jacoco.xmlReportPaths=target/report.xml'
                
            
           
    }
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
