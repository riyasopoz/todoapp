pipeline {
    agent { label 'first_agent' }  // Set the default agent for the entire pipeline
    
    stages {
        stage('Clone repository') {
            steps {
                // Checkout the source code from the SCM (Source Control Management) repository.
                checkout scm
            }
        }
        
        stage('Build image') {
            steps {
                script {
                    // Build a Docker image named "todo/test" from the Dockerfile in the checked-out repository.
                    docker.build("todo/test")
                }
            }
        }
        
        stage('Test image') {
            steps {
                script {
                    // Run tests inside the Docker container.
                    // The app.inside block runs commands inside a container based on the built image.
                    inside {
                        sh 'echo "Tests passed"'  // Placeholder for actual tests; replace with real test commands
                    }
                }
            }
        }
        
        stage('Push image') {
            steps {
                script {
                    // Authenticate with Docker Hub and push the built image, tagging it with the current build number.
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        push("${env.BUILD_NUMBER}")  // Push the image with a tag matching the build number
                    }
                }
            }
        }
        

    }
}