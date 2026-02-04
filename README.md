# Helm chart assignment

## Tools

- [Helm](https://helm.sh)
- Visual Studio Code + Kubernetes extension

## Docs

- [Getting Started | Helm](https://helm.sh/docs/chart_template_guide/getting_started/)
- [Chart Development Tips and Tricks](https://helm.sh/docs/howto/charts_tips_and_tricks/)
- [Debugging Templates](https://helm.sh/docs/chart_template_guide/debugging/)

## Useful commands

- Install: `helm install <release-name> ./gateway-chart -f values-dev.yml (-n <namespace>)`
- Upgrade: `helm upgrade <release-name> ./gateway-chart (-n <namespace>)`
    - useful flags: `--reset-then-reuse-values --atomic`
- History: `helm history <release-name> (-n <namespace>)`
- Rollback: `helm rollback <release-name> <revision> (-n <namespace>)`

## Tasks

### Task 1: Implement TODOs so the chart deploys and works.

Success criteria:
- Value `api.enabled` toggles /api route.
- Value `backend.port` controls which port nginx proxies to.
- Value `backend.text` changes the /api response.
- Value `replicaCount` affects number of pods.

#### “Definition of done” checks

- `helm lint ./gateway-chart` passes.
- `helm template ./gateway-chart` renders valid YAML.

After install:
- `/` returns gateway text
- `/api` returns backend text

### Task 2: Break stuff!

Break your app, then fix it again:
1. Upgrade the chart using `-f values-broken.yml`
2. Try to deploy using `--atomic --timeout 10s`, what happens?
3. Check the `values-broken.yml` comments
4. Answer and solve the issues one by one.

### Task 3: Other ways to make a chart

- Use `helm create <chart-name>` and start from that template.
- Can a chart depend on another chart? How does that work?

### Task 4: Installing from repository

- Charts can be installed from a repository
- Check available apps `helm search repo <repo>`
- Check available versions of specific chart `helm search repo <repo>/<chart> --versions`
- Install a given app: `helm install <repo>/<chart> --version "1.2.3."`
