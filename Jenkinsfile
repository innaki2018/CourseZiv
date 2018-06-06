pipeline{
    
    agent any

    stages{
        stage('Build'){
            steps{
		    sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
            }
	}
     
	stage('Archive'){
            steps{
                archiveArtifacts artifacts: '**/target/**/*.war, **/target/**/*.jar', fingerprint: true
            junit '**/target/**/*.xml'
            }	
        }
	    
    }
   
	
}
