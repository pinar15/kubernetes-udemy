## Network Policies

to get networkpolicy run:

```
k get netpol
```


Below policy creates network policy to allow traffic from the Internal(pod) application only to the payroll-service and db-service.



Policy Name: internal-policy

Policy Type: Egress

Egress Allow: payroll

Payroll Port: 8080

Egress Allow: mysql

MySQL Port: 3306

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
    - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080
      ```