# Template to deploy Aqua SCSP

## All options in one yaml (Don't use it please delete the options that you don't use)

```yaml
apiVersion: operator.aquasec.com/v1alpha1
kind: AquaCsp
metadata:
  name: aqua
  namespace: aqua
spec:
  requirements: true
  serviceAccount: "" # if requirements false and service account allready exists
  dbSecretName: "aqua-database-password" # if requirements false and db secret is exists
  dbSecretKey: "db-password" # if requirements false and db secret is exists
  password: "Password1" # only if requirements true DB Password Secret
  registry: # only if requirements true
    url: "registry.aquasec.com"
    username: "example@company.com"
    password: "" # Password
    email: "example@company.com"
  rbac:
    enable: true # to enable RBAC
    roleref: "" # if allready exists
    openshift: false # if using openshift
    privileged: true # if want to use privileged
  database: # if using internal DB
    replicas: 1
    service: "ClusterIP"
    image:
      repository: "database"
      registry: "registry.aquasec.com"
      tag: "4.0"
      pullPolicy: "IfNotPresent"
  externalDb: # If allready exists postgresql db and want to use an external DB
    name: "scalock"
    host: "aqua-database-svc"
    port: 5432
    username: "postgres"
    password: "example"
    auditName: "slk_audit"
    auditHost: "aqua-database-svc"
    auditPort: 5432
    auditUsername: "postgres"
    auditPassword: "example"
  gateway:
    replicas: 1
    service: "ClusterIP"
    image:
      repository: "gateway"
      registry: "registry.aquasec.com"
      tag: "4.0"
      pullPolicy: "IfNotPresent"
  server:
    replicas: 1
    service: "LoadBalancer"
    image:
      repository: "console"
      registry: "registry.aquasec.com"
      tag: "4.0"
      pullPolicy: "IfNotPresent"
  scanner:
    deploy:
      replicas: 1
      service: "ClusterIP"
      image:
        repository: "scanner"
        registry: "registry.aquasec.com"
        tag: "4.0"
        pullPolicy: "IfNotPresent"
    name: "" # If Exists and without deploy option
    min: 1
    max: 5
    imagesPerScanner: 100
  adminPassword: "Password1"
  licenseToken: # Licence
  clustermode: false
  ssl: false
  auditSsl: false
  dockerless: false
```

### Template for example

```yaml
apiVersion: operator.aquasec.com/v1alpha1
kind: AquaCsp
metadata:
  name: aqua
spec:
  requirements: true
  password: "Password1"
  rbac:
    enable: true
    openshift: false
    privileged: true
  registry:
    url: "registry.aquasec.com"
    username: "nissim.aquasec@aquasec.com"
    password: "" # Password
    email: "example@gmail.com"
  database:
    replicas: 1
    service: "ClusterIP"
    image:
      repository: "database"
      registry: "registry.aquasec.com"
      tag: "4.0"
      pullPolicy: "IfNotPresent"
  gateway:
    replicas: 1
    service: "ClusterIP"
    image:
      repository: "gateway"
      registry: "registry.aquasec.com"
      tag: "4.0"
      pullPolicy: "IfNotPresent"
  server:
    replicas: 1
    service: "LoadBalancer"
    image:
      repository: "console"
      registry: "registry.aquasec.com"
      tag: "4.0"
      pullPolicy: "IfNotPresent"
  scanner:
    deploy:
      replicas: 1
      service: "ClusterIP"
      image:
        repository: "scanner"
        registry: "registry.aquasec.com"
        tag: "4.0"
        pullPolicy: "IfNotPresent"
    min: 1
    max: 5
    imagesPerScanner: 100
  adminPassword: "Password1"
  licenseToken: # Licence
  clustermode: false
  ssl: false
  auditSsl: false
```