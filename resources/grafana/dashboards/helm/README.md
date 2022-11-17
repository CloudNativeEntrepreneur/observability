# Grafana Dashboard

This is a Helm Chart which contains Grafana dashboards, packaged in ConfigMaps by default or in a grafana-operator `datasources` custom resource if `.Values.useGrafanaOperator: true`.

This chart should be deployed alongside a Grafana chart, with the dashboards loader sidecar enabled, and the `label` configured to match.

If you want to add a dashboard, just create a new JSON file in the `dashboards` folder. Same if you want to remove/update a dashboard. The configmap template will automatically create as many configmaps as needed - which is 1 per dashboard.

## Dashboards

Name | Description | JSON file | Original Source
--- | --- | --- | ---
Cert-Manager | Displays [cert-manager](https://github.com/jetstack/cert-manager) logs & metrics, with certificates expiration dates | [cert-manager.json](dashboards/cert-manager.json) | https://grafana.com/grafana/dashboards/11001-cert-manager/

