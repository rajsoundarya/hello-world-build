pipeline {
	    agent any
	    stages {
	        stage('Build Docker Image') {
	            steps {
	                sh 'docker build -t soundy_image .'
	                }
	        }
	        stage('Deploy step') {
	            steps {
			sh 'docker rm -f java_project'
	                sh 'docker run -itd -p 8092:8080 --name java_project soundy_image'       
	            }
	        }
		stage('Push image') {
		    steps{	
		        withDockerRegistry([ credentialsId: "Docker_hub_login", url:""]) {
                    		sh 'docker tag soundy_image rajsoundarya/soundy_image:$BUILD_NUMBER'
                    		sh 'docker push rajsoundarya/soundy_image:$BUILD_NUMBER' 
                	}
        	     }
	    	}
	    }
	}
