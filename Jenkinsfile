pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=tobi-secuirty_tobisecurity -Dsonar.organization=tobi-secuirty -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=955dd153c58e6b7170195806eea712867e56a3f9'
			}
        } 

   stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
