pipeline {
    agent {
        label 'docker' // Assuming there's a Jenkins agent label named 'docker' configured to run Docker containers on Windows
    }
    triggers {
        scm('*/15 * * * *') // Poll SCM every 15 minutes
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Run Maven build inside the Docker container
                    bat 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run Maven tests inside the Docker container
                    bat 'mvn test'
                }
            }
            post {
                always {
                    // Publish JUnit test results
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                script {
                    // Specify the full path to the deliver.sh script
                    bat '.\\jenkins\\scripts\\deliver.sh'
                }
            }
        }
    }
    // Add post-build actions, notifications, etc.
}
