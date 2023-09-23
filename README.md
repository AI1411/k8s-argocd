### set project
```bash
gcloud config set project {{projectID}}
```

### get project
```bash
gcloud config get-value project
```

### create service account
```bash
gcloud iam service-accounts create gke-argocd \
  --description "used by tf" \
  --display-name "gke-argocd"
```

### add credentials to service account
```bash
gcloud projects add-iam-policy-binding {{projectID}} \
  --member serviceAccount:gke-argocd@{{projectID}}.iam.gserviceaccount.com \
  --role roles/container.admin
```

### add credentials to gke
```bash
gcloud container clusters get-credentials gke-argocd --zone asia-northeast1 --project planet-4f7c6
```

### download credentials
```bash
gcloud iam service-accounts keys create ~/.config/gcloud/account.json \
  --iam-account gke-argocd@planet-4f7c6.iam.gserviceaccount.com
```

### create app
```bash
argocd app create first-step \
  --repo https://github.com/YOUR_REPO_URL.git \
  --path PATH_TO_YOUR_MANIFEST_DIRECTORY \
  --dest-namespace NAMESPACE_YOU_WANT_TO_DEPLOY \
  --dest-server https://kubernetes.default.svc \
  --sync-policy automated
```