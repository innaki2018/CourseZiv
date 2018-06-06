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
	    
        stage('Nexus Deploy') {
	    	steps{ 
			nexusArtifactUploader(
    				nexusVersion: 'nexus2.14.8',
    				protocol: 'http',
    				nexusUrl: 'innaki-master:8081/nexus',
    				groupId: 'clinic.programming.time-tracker',
    				version: ${env.BUILD_NUMBER},
    				repository: 'Releases',
    				credentialsId: '44620c50-1589-4617-a677-7563985e46e1',
    				artifacts: [
        				[artifactId: time-tracker-web, classifier: '', 
					 file: 'time-tracker-web' + ${env.BUILD_NUMBER} + '.war', type: 'war']
    					[artifactId: time-tracker-core, classifier: '', 
					 file: 'time-tracker-core' + ${env.BUILD_NUMBER} + '.jar', type: 'jar']
    				]
 			)
        	}
	} 
	    

	    
   }
	
}