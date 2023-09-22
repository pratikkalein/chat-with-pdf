# Chat With PDF

<p align="center">
  <img src="https://raw.githubusercontent.com/pratikkalein/chat-with-pdf/main/center.png" />
</p>

Simple application using Python and Streamlit using OpenAI API. Upload any pdf file and ask questions about it! It also supports images scans.

## Screenshots
![Deployed app](/img/prod.png)

**With History and Auto generated questions**

![With History and Auto generated questions](/img/history.png)

## Local environment 
Make sure you have python and pip installed 
1. Clone the repo
```bash
git clone https://github.com/pratikkalein/chat-with-pdf
```
2. Create a virtual environment
```bash
python3 -m venv venv
```
3. Activate the enviornment 
```bash
source /venv/bin/activate
```
4. Install the requirments
```bash
pip install -r requirements.txt 
```
5. Create .env file at the root of the project and add your Open AI API key.
```
OPEN_AI_API_KEY=yourapikey
```
6. Run
```bash
streamlit run app.py
```
## Deploy to Google Cloud
### Build Docker Image using Cloud Build 

```bash
gcloud builds submit --tag gcr.io/gcp-project-id/chat-with-pdf  --project=gcp-project-id
```

### Deploy latest image to Cloud Run 

Before running the command make sure you add your secret to the Secret Manager.
Syntax for the --update-secrets
```bash
 --update-secretes=ENV_VAR_NAME=SECRET_NAME:VERSION
```

```bash
gcloud run deploy chat-with-pdf --image gcr.io/gcp-project-id/chat-with-pdf --platform managed  --project=gcp-project-id --allow-unauthenticated --region=asia-south1 --max-instances=2 --update-secrets=OPENAI_API_KEY=openai:1
```

If you wish to modify your deployment you can refere the documentation [here](https://cloud.google.com/sdk/gcloud/reference/run/deploy).