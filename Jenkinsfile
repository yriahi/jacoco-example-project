pipeline {
    agent any  // Runs on any available agent

    // tools { 
    //     // Specifies the Maven version
    //     maven 'Maven 3.6.3'
    // }

    stages {
        stage('Checkout') {
            steps {
                // Checking out code from the provided public Git repository
                git url: 'https://github.com/yriahi/jacoco-example-project.git', branch: 'main'
            }
        }

        stage('Build and Test') {
            steps {
                // Running Maven to build and test, with the JaCoCo plugin enabled for coverage
                sh 'mvn clean verify'
            }
        }

        stage('JaCoCo') {
            steps {
                // This step publishes the JaCoCo coverage report to Jenkins
                jacoco(execPattern: '**/target/jacoco.exec')
            }
        }
    }

    post {
        always {
            // Archive the build artifacts and test results
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            junit '**/target/test-*.xml'
        }
    }
}
