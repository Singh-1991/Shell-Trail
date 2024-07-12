pipeline {
    agent any

    options {
        timeout(time: 1, unit: 'HOURS')
    }

    stages {

        stage('Setup ENV ') {
            steps {
                sh "aws --version"
                withCredentials([usernamePassword(credentialsId: 'aws-credentials', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                sh """
                    export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
                    export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
                """
                }
            }
        }


        stage('Validate Hash') {
            steps {
                checkout scm // Checkout the repository into the workspace
 
                    // Enter the checked-out repository directory
                    dir("${env.WORKSPACE}/jenkins_pipeline") {
                        sh "ls -l" // List files in the repository directory.
                        sh "./ss4mm.sh" // Assuming ss4mm.sh is in the repository, execute it.
                    }
                }

            post {
                
                success {
                    echo "Verification successful. Proceeding with further stages."
                }

                failure {
                    echo "Verification failed. Failing the job."
                    currentBuild.result = 'FAILURE'
                    error "Verification failed."
                }
            }
        }
    }
}
