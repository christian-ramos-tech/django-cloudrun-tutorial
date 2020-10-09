# Django in Cloud Run

Tutorial:  
https://codelabs.developers.google.com/codelabs/cloud-run-django/index.html?index=..%2F..index#7

Google Credentials
```
export GOOGLE_APPLICATION_CREDENTIALS=./credentials.json
```

Containerize your app and upload it to Container Registry
```
gcloud builds submit --tag gcr.io/$PROJECT_ID/django-cloudrun
```

Run the migration
```
gcloud builds submit --config cloudmigrate.yaml \
    --substitutions _REGION=$REGION
```

Deploy to Cloud Run
```
gcloud run deploy django-cloudrun --platform managed --region $REGION \
  --image gcr.io/$PROJECT_ID/django-cloudrun \
  --add-cloudsql-instances ${PROJECT_ID}:${REGION}:myinstance \
  --allow-unauthenticated
```