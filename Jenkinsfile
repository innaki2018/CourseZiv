pipeline{
    
    agent any

    stages{
        stage('Build/Test'){
            steps{
                sh "cd sourceArea && mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
            }
	}
	stage('Show Tests result'){
  	    steps{ 		
	       junit '**/target/*.xml'     
 	    }		
	}
	stage('Archive'){
            steps{
                archiveArtifacts artifacts: '**/target/*.war' 
            }	
        }
    
   
   
}
