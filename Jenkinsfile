pipeline {
	    agent any
	    stages {
	        stage('Build Docker Image') {
	            steps {
	                sh 'docker build -t java_image .'
	                }
	        }
	        stage('Deploy step') {
	            steps {
			sh 'docker rm -f java_project'
	                sh 'docker run -itd -p 8091:8080 --name java_project java_image'       
	            }
	        }
		stage('Push image') {
		    steps{	
		        withDockerRegistry([ credentialsId: "Docker_hub_login", url:""]) {
                    		sh 'docker tag java_image rajsoundarya/java_image:$BUILD_NUMBER'
                    		sh 'docker push rajsoundarya/java_image:$BUILD_NUMBER' 
                	}
        	     }
	    	}
	    }
	}
