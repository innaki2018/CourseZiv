pipeline{
    
    agent any

    stages{
	    
        stage('Build'){
            steps{
		        sh 'mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package '
            }
	}
     
	stage('Results'){
            steps{
                        archiveArtifacts artifacts: '**/target/*.war, **/target/*.jar', fingerprint: true
            junit '**/target/**/*.xml'
            }	
        }
	    
	 
	stage('Sonar Analysis') { 
        	withSonarQubeEnv('Sonar') { 
				
             		sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar ' + 
          			'-f pom.xml ' +
          			'-Dsonar.projectKey=clinic.programming.time-tracker:all:master ' +
          			'-Dsonar.login=sonar ' +
          			'-Dsonar.password=unix11 ' +
          			'-Dsonar.language=java ' +
          			'-Dsonar.sources=. ' +
          			'-Dsonar.tests=. '
          			
        }
    }
	    
	    
	 stage('Nexus Deploy'){
	 	steps{
			    sh 'mvn deploy:deploy-file ' +
			    	'-DgroupId=clinic.programming.time-tracker ' +
			    	'-DartifactId=time-tracker-web ' +
			    	'-Dversion=${env.BUILD_NUMBER}-RELEASE ' + 
			    	'-DgeneratePom=true ' +
			    	'-Dpackaging=war ' +
			    	'-DrepositoryId=nexus ' + 
			    	'-Durl=http://innaki-master:8081/nexus/content/repositories/releases ' + 
				'-Dfile=web/target/.war '
					}
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
        				[artifactId: time-tracker-web, classifier: '', extension: '',
					 file: 'time-tracker-web' + '${BUILD_NUMBER}' + '-RELEASE' '.war', type: 'war']
    					[artifactId: time-tracker-core, classifier: '', extension: '',
					 file: 'time-tracker-core' + '${BUILD_NUMBER}' + '-RELEASE' + '.jar', type: 'jar']
    				]
 			)
        	}
	} */
	    
	    

	    
   }
	
}
