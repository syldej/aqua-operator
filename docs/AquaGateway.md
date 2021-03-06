# Template to deploy Aqua Gateway

# All option in one Template (Don't use it please delete the options that you don't use)

```yaml
apiVersion: operator.aquasec.com/v1alpha1
kind: AquaGateway
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
  deploy:
    replicas: 1
    service: "ClusterIP"
    image:
      repository: "gateway"
      registry: "registry.aquasec.com"
      tag: "3.5"
      pullpolicy: "IfNotPresent"
  aquaDb: "aqua-database" # if aqua database allready exists
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
  ssl: false
  auditSsl: false
  openshift: false
```

### Template for example

```yaml
apiVersion: operator.aquasec.com/v1alpha1
kind: AquaGateway
metadata:
  name: aqua
spec:
  requirements: false
  serviceAccount: "aqua-sa"
  dbSecretName: "aqua-database-password"
  dbSecretKey: "db-password"
  deploy:
    replicas: 1
    service: "ClusterIP"
    image:
      repository: "gateway"
      registry: "registry.aquasec.com"
      tag: "3.5"
      pullpolicy: "IfNotPresent"
  aquaDb: "aqua-database"
  ssl: false
  auditSsl: false
  openshift: false
```