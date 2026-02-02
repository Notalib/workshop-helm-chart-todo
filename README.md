# Helm chart assignment

## Deliverables

Implement the TODOs so the chart deploys a working gateway.

Must support:
- api.enabled toggles /api route
- backend.port controls where nginx proxies
- backend.text changes the /api response
- replicaCount affects number of pods

## “Definition of done” checks

- `helm lint ./gateway-chart` passes
- `helm template ./gateway-chart` renders valid YAML

After install:
- / returns gateway text
- /api returns backend text

Break/fix:
- Change backend.port to wrong value → /api becomes 502 while / still works
- Change it back → /api works again

Suggested flow

1. Start with Deployment (pods running)
2. Add ConfigMap mount (nginx starts)
3. Add Service
4. Add Ingress
5. Then do the break/fix exercise
