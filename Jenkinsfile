pipeline{
    
    agent any

    stages{
	    
        stage('Build'){
            steps{
		        sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
            }
	}
     
	stage('Results'){
            steps{
                        archiveArtifacts artifacts: '**/target/*.war, **/target/*.jar', fingerprint: true
            junit '**/target/**/*.xml'
            }	
        }
	    
        stage('Publish') {
	    	steps{ 
                   	nexusArtifactUploader {
        			nexusVersion('nexus2.14.8')
        			protocol('http')
        			nexusUrl('innaki-master:8081/nexus')
        			groupId('clinic.programming.time-tracker')
        			version('${env.BUILD_NUMBER}')
        			repository('releases')
        			credentialsId('44620c50-1589-4617-a677-7563985e46e1')
        			artifact {
            				artifactId('time-tracker-web')
           				type('war')
            				classifier('')
            				file('time-tracker-web.war')
      				}
        			artifact {
            				artifactId('time-tracker-core')
            				type('jar')
            				classifier('')
            				file('time-tracker-core.jar')
        			}
      			}
    		}
	} 
	    

	    
   }
}
