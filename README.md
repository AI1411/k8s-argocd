### create app
```bash
argocd app create first-step \
  --repo https://github.com/YOUR_REPO_URL.git \
  --path PATH_TO_YOUR_MANIFEST_DIRECTORY \
  --dest-namespace NAMESPACE_YOU_WANT_TO_DEPLOY \
  --dest-server https://kubernetes.default.svc \
  --sync-policy automated

```