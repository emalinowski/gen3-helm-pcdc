# amanuensis

![Version: 0.1.2](https://img.shields.io/badge/Version-0.1.2-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart for Kubernetes

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| file://../common | common | 0.1.11 |
| https://charts.bitnami.com/bitnami | postgresql | 11.9.13 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| AWS_CREDENTIALS.AWS_SES.AWS_REGION | string | `"us-east-1"` |  |
| AWS_CREDENTIALS.AWS_SES.RECIPIENT | string | `""` |  |
| AWS_CREDENTIALS.AWS_SES.SENDER | string | `""` |  |
| AWS_CREDENTIALS.AWS_SES.aws_access_key_id | string | `""` |  |
| AWS_CREDENTIALS.AWS_SES.aws_secret_access_key | string | `""` |  |
| AWS_CREDENTIALS.DATA_DELIVERY_S3_BUCKET.aws_access_key_id | string | `""` |  |
| AWS_CREDENTIALS.DATA_DELIVERY_S3_BUCKET.aws_secret_access_key | string | `""` |  |
| AWS_CREDENTIALS.DATA_DELIVERY_S3_BUCKET.bucket_name | string | `""` |  |
| CSL_KEY | string | `""` |  |
| affinity | object | `{}` |  |
| arboristUrl | string | `nil` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| commonLabels | map | `nil` | Will completely override the commonLabels defined in the common chart's _label_setup.tpl |
| criticalService | string | `"true"` | Valid options are "true" or "false". If invalid option is set- the value will default to "false". |
| datadogLogsInjection | bool | `true` | If enabled, the Datadog Agent will automatically inject Datadog-specific metadata into your application logs. |
| datadogProfilingEnabled | bool | `true` | If enabled, the Datadog Agent will collect profiling data for your application using the Continuous Profiler. This data can be used to identify performance bottlenecks and optimize your application. |
| datadogTraceSampleRate | int | `1` | A value between 0 and 1, that represents the percentage of requests that will be traced. For example, a value of 0.5 means that 50% of requests will be traced. |
| env | list | `[{"name":"GEN3_UWSGI_TIMEOUT","valueFrom":{"configMapKeyRef":{"key":"uwsgi-timeout","name":"manifest-global","optional":true}}},{"name":"AWS_STS_REGIONAL_ENDPOINTS","value":"regional"},{"name":"PYTHONPATH","value":"/var/www/amanuensis"},{"name":"GEN3_DEBUG","value":"False"},{"name":"AMANUENSIS_PUBLIC_CONFIG","valueFrom":{"configMapKeyRef":{"key":"amanuensis-config-public.yaml","name":"manifest-amanuensis","optional":true}}}]` | Environment variables to pass to the container |
| externalSecrets | map | `{"amanuensisConfig":null,"amanuensisJwtKeys":null,"createK8sAmanuensisConfigSecret":false,"createK8sJwtKeysSecret":false}` | External Secrets settings. |
| externalSecrets.amanuensisConfig | string | `nil` | Will override the name of the aws secrets manager secret. Default is "fence-config" |
| externalSecrets.amanuensisJwtKeys | string | `nil` | Will override the name of the aws secrets manager secret. Default is "fence-jwt-keys" |
| externalSecrets.createK8sAmanuensisConfigSecret | string | `false` | Will create the Helm "fence-config" secret even if Secrets Manager is enabled. This is helpful if you are wanting to use External Secrets for some, but not all secrets. |
| externalSecrets.createK8sJwtKeysSecret | string | `false` | Will create the Helm "fence-jwt-keys" secret even if Secrets Manager is enabled. This is helpful if you are wanting to use External Secrets for some, but not all secrets. |
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
| image.repository | string | `"quay.io/pcdc/amanuensis"` |  |
| image.tag | string | `"pcdc_dev_2023-09-06T16_36_49-05_00"` |  |
| imagePullSecrets | list | `[]` |  |
| logo | string | `nil` |  |
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
| resources.limits | map | `{"cpu":1,"memory":"512Mi"}` | The maximum amount of resources that the container is allowed to use |
| resources.limits.cpu | string | `1` | The maximum amount of CPU the container can use |
| resources.limits.memory | string | `"512Mi"` | The maximum amount of memory the container can use |
| resources.requests.cpu | string | `0.1` | The amount of CPU requested |
| resources.requests.memory | string | `"12Mi"` | The amount of memory requested |
| securityContext | object | `{}` |  |
| selectorLabels | map | `nil` | Will completely override the selectorLabels defined in the common chart's _label_setup.tpl |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |
| volumeMounts | list | `[{"mountPath":"/amanuensis/amanuensis/static/img/logo.svg","name":"logo-volume","readOnly":true,"subPath":"logo.svg"},{"mountPath":"/var/www/amanuensis/amanuensis-config.yaml","name":"config-volume","readOnly":true,"subPath":"amanuensis-config.yaml"},{"mountPath":"/var/www/amanuensis/yaml_merge.py","name":"yaml-merge","readOnly":true,"subPath":"yaml_merge.py"},{"mountPath":"/var/www/amanuensis/creds.json","name":"amanuensis-volume","readOnly":true,"subPath":"creds.json"},{"mountPath":"/var/www/amanuensis/jwt_private_key.pem","name":"amanuensis-jwt-keys","readOnly":true,"subPath":"jwt_private_key.pem"}]` | Volumes to mount to the container. |
| volumes | list | `[{"configMap":{"name":"logo-config"},"name":"logo-volume"},{"name":"config-volume","secret":{"secretName":"amanuensis-config"}},{"name":"amanuensis-volume","secret":{"secretName":"amanuensis-creds"}},{"name":"amanuensis-jwt-keys","secret":{"items":[{"key":"jwt_private_key.pem","path":"jwt_private_key.pem"}],"secretName":"amanuensis-jwt-keys"}},{"configMap":{"name":"amanuensis-yaml-merge","optional":true},"name":"yaml-merge"}]` | Volumes to attach to the container. |
