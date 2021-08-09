pipeline {
  agent any
  environment {
    PROJECT_ID = 'acn-qe-accelerators'
    REGION = 'us-east1'
    SERVACC = 'pe-jenkins@acn-qe-accelerators.iam.gserviceaccount.com'
    KEYFILE = 'acn-qe-accelerators-99fdcf4faba3.json'
    CHAOS_CLUSTER = 'jenkins-gke-auto-app'
    JMETER_CLUSTER = 'jenkins-gke-auto-app'
    DVMA_FILENAME = 'dvwa-deployment-pe'
    CHAOS_MESH_RBAC_FILENAME = 'chaos-dashboard-cluster-admin-rbac.yaml'
    CHAOS_ATTACK_FILENAME = 'chaos-action-pod-failure.yaml'
    JMETER_MASTER_FILENAME = 'jmeter-master.yaml'
    JMETER_WORKER_FILENAME = 'jmeter-worker.yaml'
    JMX_FILENAME = 'PE_Demo_dvwa-app.jmx'
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
          gcloud auth activate-service-account $SERVACC --key-file=/home/jenkins/$KEYFILE
          echo "Enable Container APIs"
          gcloud services enable container.googleapis.com
          gcloud container clusters get-credentials "$CHAOS_CLUSTER" --region="$REGION" --project "$PROJECT_ID"
          gcloud container images list
          kubectl run hi --image=gcr.io/hello-world
          kubectl get pods
          #kubectl apply -f ./$JMETER_MASTER_FILENAME
        '''
      }
    }
  }
}
