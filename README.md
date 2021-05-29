# cloud-run-update-env-from-file
Script for updating environmental variables of cloud run service using yaml file

First, install gcloud-sdk
https://cloud.google.com/sdk/docs/install

Initialize SDK
https://cloud.google.com/sdk/docs/initializing

Authorize SDK
https://cloud.google.com/sdk/docs/authorizing

Download service yaml configuration
```sh
gcloud run services describe <SERVICE_NAME> --format export > service.yml
```

Add environmental variables to the service
```sh
python add_env_to_service_file.py --env-file=.env.yaml --service-file=service.yaml --out=new_service.yml
```

Replace service with created one
```sh
gcloud beta run services replace new_service.yml
```
