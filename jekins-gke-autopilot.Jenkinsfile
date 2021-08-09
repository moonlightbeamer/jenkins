pipeline {
  agent any
  environment {
    PROJECT_ID = 'acn-qe-accelerators'
    REGION = 'us-east1'
    CHAOS_CLUSTER = 'jenkins-gke-auto-app'
    JMETER_CLUSTER = 'jenkins-gke-auto-app'
  }
  stages {
    stage ('first') {
      steps {
        sh '''
          echo 'hello'
          pwd
          ls -la
          echo "Jenkins Build Agent's IP = $(curl -s ifconfig.co)"
          echo "Jenkins Build Agent's Hostname = $(hostname -f)"
          echo "Enable Container APIs"
          gcloud services enable container.googleapis.com
          gcloud container clusters get-credentials "$CHAOS_CLUSTER" --region="$REGION" --project "$PROJECT_ID"
        '''
      }
    }
  }
}
