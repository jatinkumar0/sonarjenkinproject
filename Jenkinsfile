// pipeline {

// agent any

// //stages{

// //stage()  pipeline {
// //     agent {
// //         docker {
// //             image 'maven:3.8.1-jdk-8'
// //             args '-v /root/.m2:/root/.m2'
// // 	          args '-v /opt/:/opt/'
// //         }
// //     }
// 	  stages{
//      	    stage('Code Compile'){
//     steps{
// 	sh 'mvn compile'
//     }
// 	}
// 	    stage('Code Build') {
//             steps {
//                 sh 'mvn clean install'
//             }
//         }
// 	           stage('Unit Test') {
// steps {
//     sh 'mvn test'
// }
// post {
// always {
// junit allowEmptyResults: true, testResults : 'target/*.xml'
// }
// }
// }
// //     stage('Integration test') {
// //                 steps {
// //                 sh 'mvn test -Dtest=**/*IT.java'
// //             }
// //         }
	      
//  stage('SonarQube Analysis') {
//                     steps {
//            withSonarQubeEnv(credentialsId: "sonar", installationName: "sonar")
//         {  
//         sh 'java -jar jacococli.jar report target/jacoco.exec --classfiles target/  --xml target/report.xml'
//            sh 'mvn sonar:sonar \
//                     -Dsonar.tests=src/test/ \
//            -Dsonar.junit.reportsPath=target/ \
//             -Dsonar.coverage.jacoco.xmlReportPaths=target/report.xml'
                
            
           
//     }
//             }
//             }
// 	     	  	    stage('Deploy')
// 	    {
// 		    steps
// 		    {
// 			sh 'mvn package spring-boot:repackage'
// 		    }
// 	    }

// 	        stage('Backup')
// 	    {
// 		    steps{
// 			    sh 'mv target/sampleapp-1.0.0-SNAPSHOT-LOCAL.jar target/01.$BUILD_NUMBER.jar'
// 			    sh 'cp target/01.$BUILD_NUMBER.jar /opt/backup/'
			    
// 			    }
// 	    }
//    }
// }

// {


// }


// }

// }
pipeline {
    agent any
    stages {
        stage ('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage ('build code'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage ('test'){
            steps{
                sh 'touch test-results-unit.xml'
                sh 'mvn test'
            }
           post{
                always{
                   junit 'test-results-unit.xml'
               }
           }
        }
        stage('sonarqube integration') {
				steps {
					withSonarQubeEnv(credentialsId: 'sonar', installationName: 'sonar'){
				       sh 'mvn sonar:sonar'
					}
				}
        }
//         stage ('Create WAR file'){
//             steps{
//                 sh 'jar -cf target/dependency/webapp-runner.jar target/*.war'
//             }
//         }
//         stage ('Upload to S3'){
//             steps{
//                 s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'tf-task-s3', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**/target/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'UNSTABLE', profileName: 'ct-deepak-aws', userMetadata: []
//             }
//         }
//         stage ('Archieve the artifact'){
//             steps{
//                 archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
//             }
//         }
    }
}
