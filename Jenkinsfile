pipeline {
	agent any
 	environment {
		// DOCKER_TAG = getDockerTag()
                WAR_NAME = 'SimpleJavaWebProject-1.0-SNAPSHOT.war' // Change as needed
                TOMCAT_URL = 'http://localhost:8080' // Change for your setup
                DEPLOY_PATH = '/webapps' // Tomcat context path
		ENV = 'develop'
		DOCKERHUB_CREDENTIALS_ID = "7f9ba4ff-b64d-4cc4-8518-ee8d0d60ae73"
        }
	stages {
		stage('checkout') {
			steps {
		             // start with  clean workspce
			     deleteDir()
		             //checkout branch
		             checkout scm
			}
		}
		stage('build') {
			steps {
			    bat 'mvn clean package'
				//sh "mvn clean package -DskipTests -Djacoco.skip=true"
		        //sh "docker build . -t  skr1819/skrknowledge/${ENV}"
			}
		}

		
		
		stage('Deploy to Tomcat') {
                        steps {
                               withCredentials([usernamePassword(credentialsId: 'TOMCAT_CRED', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASS')]) {
                    bat """
                    curl -u %TOMCAT_USER%:%TOMCAT_PASS% ^
                         --upload-file target\\%WAR_NAME% ^
                         "%TOMCAT_URL%/manager/text/deploy?path=%DEPLOY_PATH%&update=true"
                    """
                   }
                }
	     }
			//stage('Docker build image && push') {
		//	steps {
			    //script {
			      // docker.withRegistry('https://registry.hub.docker.com', "${DOCKERHUB_CREDENTIALS_ID}") {
                    //   sh "docker push skr1819/skrknowledge/${ENV}:latest"
                   //}
			    //}
		//	}
		//}
		//stage('deploy to kuberneters') {
		//	steps {
		//		sh "docker images"
		//	}
		//}
    }
}
