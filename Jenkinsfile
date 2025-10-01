pipeline {
  agent any
  tools { 
        maven 'maven_3.8.4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=danbuggywebapp -Dsonar.organization=danbuggywebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=e99690280307fc919f4a959d403aca974f70ff06'
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
