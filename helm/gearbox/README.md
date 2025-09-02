# gearbox

![Version: 0.1.1](https://img.shields.io/badge/Version-0.1.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart for Kubernetes

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| file://../common | common | 0.1.11 |
| https://charts.bitnami.com/bitnami | postgresql | 11.9.13 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| commonLabels | map | `nil` | Will completely override the commonLabels defined in the common chart's _label_setup.tpl |
| criticalService | string | `"true"` | Valid options are "true" or "false". If invalid option is set- the value will default to "false". |
| datadogLogsInjection | bool | `true` | If enabled, the Datadog Agent will automatically inject Datadog-specific metadata into your application logs. |
| datadogProfilingEnabled | bool | `true` | If enabled, the Datadog Agent will collect profiling data for your application using the Continuous Profiler. This data can be used to identify performance bottlenecks and optimize your application. |
| datadogTraceSampleRate | int | `1` | A value between 0 and 1, that represents the percentage of requests that will be traced. For example, a value of 0.5 means that 50% of requests will be traced. |
| env[0].name | string | `"GEN3_DEBUG"` |  |
| env[0].value | string | `"False"` |  |
| env[1].name | string | `"GEN3_ES_ENDPOINT"` |  |
| env[1].value | string | `"http://esproxy-service:9200"` |  |
| env[2].name | string | `"AWS_REGION"` |  |
| env[2].value | string | `"us-east-1"` |  |
| env[3].name | string | `"GB_SECRET_READY"` |  |
| env[3].valueFrom.secretKeyRef.key | string | `"secretready"` |  |
| env[3].valueFrom.secretKeyRef.name | string | `"gearbox-g3auto"` |  |
| env[3].valueFrom.secretKeyRef.optional | bool | `false` |  |
| fullnameOverride | string | `""` |  |
| global.ddEnabled | bool | `false` | Whether Datadog is enabled. |
| global.dev | bool | `true` | Whether the deployment is for development purposes. |
| global.dictionaryUrl | string | `"https://s3.amazonaws.com/dictionary-artifacts/datadictionary/develop/schema.json"` | URL of the data dictionary. |
| global.dispatcherJobNum | int | `10` | Number of dispatcher jobs. |
| global.environment | string | `"default"` | Environment name. This should be the same as vpcname if you're doing an AWS deployment. Currently this is being used to share ALB's if you have multiple namespaces. Might be used other places too. |
| global.hostname | string | `"localhost"` | Hostname for the deployment. |
| global.kubeBucket | string | `"kube-gen3"` | S3 bucket name for Kubernetes manifest files. |
| global.logsBucket | string | `"logs-gen3"` | S3 bucket name for log files. |
| global.minAvialable | int | `1` | The minimum amount of pods that are available at all times if the PDB is deployed. |
| global.netPolicy | bool | `{"enabled":false}` | Whether network policies are enabled. |
| global.pdb | bool | `false` | If the service will be deployed with a Pod Disruption Budget. Note- you need to have more than 2 replicas for the pdb to be deployed. |
| global.portalApp | string | `"gitops"` | Portal application name. |
| global.postgres | map | `{"dbCreate":true,"master":{"host":null,"password":null,"port":"5432","username":"postgres"}}` | Postgres database configuration. |
| global.postgres.dbCreate | bool | `true` | Whether the database should be created. |
| global.postgres.master | map | `{"host":null,"password":null,"port":"5432","username":"postgres"}` | Master credentials to postgres. This is going to be the default postgres server being used for each service, unless each service specifies their own postgres |
| global.postgres.master.host | string | `nil` | hostname of postgres server |
| global.postgres.master.password | string | `nil` | password for superuser in postgres. This is used to create or restore databases |
| global.postgres.master.port | string | `"5432"` | Port for Postgres. |
| global.postgres.master.username | string | `"postgres"` | username of superuser in postgres. This is used to create or restore databases |
| global.publicDataSets | bool | `true` | Whether public datasets are enabled. |
| global.revproxyArn | string | `"arn:aws:acm:us-east-1:123456:certificate"` | ARN of the reverse proxy certificate. |
| global.syncFromDbgap | bool | `false` | Whether to sync data from dbGaP. |
| global.tierAccessLevel | string | `"libre"` | Access level for tiers. acceptable values for `tier_access_level` are: `libre`, `regular` and `private`. If omitted, by default common will be treated as `private` |
| global.tierAccessLimit | int | `1000` | Only relevant if tireAccessLevel is set to "regular". Summary charts below this limit will not appear for aggregated data. |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"quay.io/pcdc/gearbox_be"` |  |
| image.tag | string | `"1.3.0"` |  |
| imagePullSecrets | list | `[]` |  |
| initVolumeMounts[0].mountPath | string | `"/src/.env"` |  |
| initVolumeMounts[0].name | string | `"config-volume-g3auto"` |  |
| initVolumeMounts[0].readOnly | bool | `true` |  |
| initVolumeMounts[0].subPath | string | `"gearbox.env"` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| partOf | string | `"Core-Service"` | Label to help organize pods and their use. Any value is valid, but use "_" or "-" to divide words. |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| postgres.database | string | `nil` | Database name for postgres. This is a service override, defaults to <serviceName>-<releaseName> |
| postgres.dbCreate | bool | `nil` | Whether the database should be created. Default to global.postgres.dbCreate |
| postgres.dbRestore | bool | `false` |  |
| postgres.host | string | `nil` | Hostname for postgres server. This is a service override, defaults to global.postgres.host |
| postgres.password | string | `nil` | Password for Postgres. Will be autogenerated if left empty. |
| postgres.port | string | `"5432"` | Port for Postgres. |
| postgres.separate | string | `false` | Will create a Database for the individual service to help with developing it. |
| postgres.username | string | `nil` | Username for postgres. This is a service override, defaults to <serviceName>-<releaseName> |
| postgresql.primary.persistence.enabled | bool | `false` | Option to persist the dbs data. |
| release | string | `"production"` | Valid options are "production" or "dev". If invalid option is set- the value will default to "dev". |
| replicaCount | int | `1` |  |
| resources.limits.cpu | int | `1` |  |
| resources.limits.memory | string | `"2048Mi"` |  |
| resources.requests.cpu | float | `0.4` |  |
| resources.requests.memory | string | `"512Mi"` |  |
| securityContext | object | `{}` |  |
| selectorLabels | map | `nil` | Will completely override the selectorLabels defined in the common chart's _label_setup.tpl |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |
| volumeMounts[0].mountPath | string | `"/src/src/gearbox/keys/jwt_public_key.pem"` |  |
| volumeMounts[0].name | string | `"gearbox-middleware-jwt-keys"` |  |
| volumeMounts[0].readOnly | bool | `true` |  |
| volumeMounts[0].subPath | string | `"jwt_public_key.pem"` |  |
| volumeMounts[1].mountPath | string | `"/src/.env"` |  |
| volumeMounts[1].name | string | `"config-volume-g3auto"` |  |
| volumeMounts[1].readOnly | bool | `true` |  |
| volumeMounts[1].subPath | string | `"gearbox.env"` |  |
| volumeMounts[2].mountPath | string | `"/aggregate_config.json"` |  |
| volumeMounts[2].name | string | `"config-volume"` |  |
| volumeMounts[2].readOnly | bool | `true` |  |
| volumeMounts[2].subPath | string | `"aggregate_config.json"` |  |
| volumeMounts[3].mountPath | string | `"/gearbox.json"` |  |
| volumeMounts[3].name | string | `"config-manifest"` |  |
| volumeMounts[3].readOnly | bool | `true` |  |
| volumeMounts[3].subPath | string | `"json"` |  |
| volumes[0].name | string | `"gearbox-middleware-jwt-keys"` |  |
| volumes[0].secret.items[0].key | string | `"jwt_public_key.pem"` |  |
| volumes[0].secret.items[0].path | string | `"jwt_public_key.pem"` |  |
| volumes[0].secret.secretName | string | `"gearbox-middleware-jwt-keys"` |  |
| volumes[1].name | string | `"config-volume-g3auto"` |  |
| volumes[1].secret.secretName | string | `"gearbox-g3auto"` |  |
| volumes[2].name | string | `"config-volume"` |  |
| volumes[2].secret.optional | bool | `true` |  |
| volumes[2].secret.secretName | string | `"gearbox-config"` |  |
| volumes[3].configMap.name | string | `"manifest-gearbox"` |  |
| volumes[3].configMap.optional | bool | `true` |  |
| volumes[3].name | string | `"config-manifest"` |  |
