# Helm chart assignment

## Tools

- [Helm CLI tool](https://helm.sh)
- Recommended editor: Visual Studio Code + Kubernetes extension

## Docs

- [Getting Started | Helm](https://helm.sh/docs/chart_template_guide/getting_started/)
- [Chart Development Tips and Tricks](https://helm.sh/docs/howto/charts_tips_and_tricks/)
- [Debugging Templates](https://helm.sh/docs/chart_template_guide/debugging/)

## Useful commands

- Create chart skeleton: `helm create <chart-name>`
- Install chart: `helm install <release-name> ./gateway-chart -f values-dev.yml (-n <namespace>)`
- Upgrade chart: `helm upgrade <release-name> ./gateway-chart (-n <namespace>)`
    - useful flags: `--reset-values --atomic`
- Release history: `helm history <release-name> (-n <namespace>)`
- Release rollback: `helm rollback <release-name> <revision> (-n <namespace>)`

## Tasks

### Task 1: Install and experiment with `simplest-chart`

Demos the absolute basics of a Helm chart.
`simple-chart` only has a single kubernetes Deployment, a ConfigMap and 2 template values.

1. Install: `helm install simple ./simplest-chart`
2. Test the deployment: `kubectl port-forward deploy/simplest-nginx 8888:80`
3. Enable HTML override: `helm upgrade simple ./simplest-chart --set overrideHtml=true`
4. What happened to the deployment's website? Try changing the HTML in the ConfigMap
6. Change image: `helm upgrade simple ./simplest-chart --set imageTag=stable`
7. Uninstall: `helm uninstall simple`

In the above commands `simple` is the release-name. It can be installed several times under different names & namespaces.

Try installing in a different namespace:
1. Create namespace: `kubectl create namespace demo`
2. Install into namespace: `helm install simple ./simplest-chart --namespace demo`, what happens?

### Task 2: Implement TODOs in `gateway-chart`

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

### Task 3: Break stuff!

Break your app, then fix it again:
1. Upgrade the chart using `-f values-broken.yml`
2. Try to deploy using `--atomic --timeout 10s`, what happens?
3. Check the `values-broken.yml` comments
4. Answer and solve the issues one by one.

### Task 5: Installing from repository

- Charts can be installed from a repository
- Check available apps `helm search repo <repo>`
- Check available versions of specific chart `helm search repo <repo>/<chart> --versions`
- Install a given app: `helm install <repo>/<chart> --version "1.2.3."`

Suggested repos you can add:
- https://helm.github.io/examples (hello-world app)
- https://helm.elastic.co (elasticsearch)
- https://charts.gitlab.io/ (gitlab)
- https://github.com/cdwv/awesome-helm?tab=readme-ov-file#repositories--hubs
