pipeline{
    
    agent any

    stages{
	    
        stage('Build'){
            steps{
		        sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
            }
	}
     
	stage('Check Results'){
            steps{
                        archiveArtifacts artifacts: '**/target/*.war, **/target/*.jar', fingerprint: true
            junit '**/target/**/*.xml'
            }	
        }
	    
	    
	stage('Publish') {
     		nexusPublisher nexusInstanceId: 'localNexus', 
			nexusRepositoryId: 'releases', 
			packages: [[$class: 'MavenPackage', 
				    mavenAssetList: [[classifier: '', 
						      extension: 'RELEASE', 
						      filePath: 'web/target/*.war']], 
				    mavenCoordinate: [artifactId: 'time-tracker-web', 
						      groupId: 'clinic.programming.time-tracker', 
						      packaging: 'war', version: '${BUILD_NUMBER}']]]
   	}
	    
	    
        /*stage('Nexus Deploy') {
	    	steps{ 
						
			nexusArtifactUploader(
    				nexusVersion: 'nexus2.14.8',
    				protocol: 'http',
    				nexusUrl: 'innaki-master:8081/nexus',
    				groupId: 'clinic.programming.time-tracker',
				version: '${BUILD_NUMBER}',
    				repository: 'Releases',
    				credentialsId: '44620c50-1589-4617-a677-7563985e46e1',
    				artifacts: [
        				[artifactId: time-tracker-web, classifier: '', extension: 'RELEASE',
					 file: 'time-tracker-web' + '${BUILD_NUMBER}' + '.war', type: 'war']
    					[artifactId: time-tracker-core, classifier: '', extension: 'RELEASE',
					 file: 'time-tracker-core' + '${BUILD_NUMBER}' + '.jar', type: 'jar']
    				]
 			)
        	}
	} */
	    
	    

	    
   }
	
}
