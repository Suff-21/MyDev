pipeline {
    agent any

    tools {
        // Specify Maven version installed on Jenkins
        maven 'Maven 3'
        // Specify JDK version if needed
        jdk 'OpenJDK 11'
    }

    environment {
        // Set any environment variables here
        MVN_HOME = tool name: 'Maven 3', type: 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git
                git url: 'https://github.com/your-username/your-repository.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean install
                script {
                    sh "'${MVN_HOME}/bin/mvn' clean install"
                }
            }
        }

        stage('Test') {
            steps {
                // Run Maven tests (optional, can be part of build step)
                script {
                    sh "'${MVN_HOME}/bin/mvn' test"
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy to an environment using Ansible (Example: run an Ansible playbook)
                // Ensure Ansible is installed on Jenkins and configured
                script {
                    sh 'ansible-playbook -i inventory/hosts deploy.yml'
                }
            }
        }
    }

    post {
        success {
            // Actions to take if the build is successful
            echo 'Build completed successfully!'
        }
        failure {
            // Actions to take if the build fails
            echo 'Build failed!'
        }
    }
}
