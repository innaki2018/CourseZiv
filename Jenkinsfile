pipeline{
    
    agent any

    stages{
        stage('Build'){
            steps{
		    sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
            }
	}
     
	stage('Tests'){
  	    steps{ 		
	       junit '**/target/*.xml'     
 	    }		
	}
	
	 stage('Archive'){
            steps{
                archiveArtifacts artifacts: '**/target/*.war','**/target/*.jar' 
            }	
        }

    }
   
}
