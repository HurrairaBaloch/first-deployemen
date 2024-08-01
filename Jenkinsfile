pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS' // Use the name you set in Global Tool Configuration
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                dir('frontend') {
                    sh 'npm ci' // Use 'ci' instead of 'install' for cleaner, more reliable builds
                }
            }
        }
        
        stage('Lint') {
            steps {
                dir('frontend') {
                    sh 'npm run lint' // Assuming you have a lint script in package.json
                }
            }
        }
        
        stage('Test') {
            steps {
                dir('frontend') {
                    sh 'npm test -- --watchAll=false' // Run tests in non-interactive mode
                }
            }
        }
        
        stage('Build') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                dir('frontend') {
                    archiveArtifacts artifacts: 'build/**', fingerprint: true
                }
            }
        }
        
        stage('Deploy') {
            steps {
                // Add your deployment steps here
                // This is just a placeholder
                dir('frontend') {
                    sh 'echo "Deploying the application..."'
                    // Example: sh 'aws s3 sync build/ s3://your-bucket-name/'
                }
            }
        }
    }
    
    post {
        always {
            cleanWs() // Clean up workspace after build
        }
    }
}