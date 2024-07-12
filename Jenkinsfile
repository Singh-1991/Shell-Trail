pipeline {
  agent any

  stages {
    stage('ENV setup') {
      sh "aws --version"
      // Below step uses the secrets from Jenkins secrets.
      withCredentials([usernamePassword(credentialsId: 'aws-credentials', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
      sh """
           export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
           export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
      """
    }
    
    stage('CheckOut Code'){
      git URL: 
    }

    [3:58 PM] Balaji, Siva Kumar S
stage('Validate Hash') {
            steps {
                container('awscli-image') {
                    checkout scm  // Checkout the SCM to get the 'jenkins_pipeline' directory
 
                    dir("${env.WORKSPACE}/jenkins_pipeline") {
                        sh "chmod +x verify_hash.sh"
                        sh "./verify_hash.sh"
                    }
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
