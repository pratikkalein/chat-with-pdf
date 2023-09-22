pipeline {
    agent any
    
     environment {
        GCP_PROJECT_ID     = credentials('gcp_project_id')
        GCP_SECRET         = credentials('gcp_secret')
        GCP_SERVICE_ACCOUNT = credentials('gcp_service_account')
        
    }

    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', poll: false, url: 'https://github.com/pratikkalein/chat-with-pdf'
            }
        
        }
        
        stage('Cloud Build') {
            steps {
                sh 'gcloud auth activate-service-account --key-file=${GCP_SERVICE_ACCOUNT}'
                sh 'gcloud builds submit --tag gcr.io/${GCP_PROJECT_ID}/chat-with-pdf  --project=${GCP_PROJECT_ID}'
            }
        
        }
        
        stage('Cloud Deploy') {
            steps {
                sh 'gcloud run deploy chat-with-pdf --image gcr.io/${GCP_PROJECT_ID}/chat-with-pdf --platform managed  --project=${GCP_PROJECT_ID} --allow-unauthenticated --region=asia-south1 --max-instances=1 --update-secrets=OPENAI_API_KEY=${GCP_SECRET}:1'
            }
        
        }
    }
}
