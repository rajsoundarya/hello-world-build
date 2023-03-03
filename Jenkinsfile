pipeline {
	    agent any
	    stages {
		stage('test') {
	            steps {
	                sh 'docker images'
	             }
	        }
	        stage('Build Docker Image') {
	            steps {
	                sh 'docker build -t java_image .'
	                }
	        }
	        stage('Deploy step') {
	            steps {
			sh 'docker rm -f java_container'
	                sh 'docker run -itd -p 8091:8080 --name java_container java_image'       
	            }
	        }
		stage('Push image') {
		    steps{	
		        script{ 
        		    withDockerRegistry([ credentialsId: "Docker_hub_login", url: "" ]) {
        		  	dockerImage.push("1.0")
			    }
		        }
        	     }
	    	}
	    }
	}
