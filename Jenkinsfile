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
	                sh 'docker run -itd -p 8090:8080 --name java_container java_image'       
	            }
	        }
		stage('Push image') {
		    steps{	
			script{ 
        			withDockerRegistry([ credentialsId: "Docker_hub_login", url: "" ]) {
        		     		dockerImage.push("1.0")
				}
			}
			sh 'docker rm -f java_image'
		    }
        	}
	     }
	}
