**Name**: user-name

**Slack User ID**: 00000000000

**Email**: user-email@example.com   

---

## Solution

### Solution Details

(Explain your approach, thought process, and steps you took to solve the challenge)

### Code Snippet

```yaml
# Place your code or configuration snippet here

apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: dev-app
  template:
    metadata:
      labels:
        app: dev-app
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: environment
                operator: In
                values:
                - development
      containers:
      - name: nginx
        image: nginx:latest

---


apiVersion: apps/v1
kind: Deployment
metadata:
  name: production-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prod-app
  template:
    metadata:
      labels:
        app: prod-app
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: environment
                operator: In
                values:
                - production
      containers:
      - name: nginx
        image: nginx:latest