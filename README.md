In order to test, run the following:

```
cd foobar2
helm template test . --namespace=default
helm template test . --namespace=default --set foobar.app.resources.limits.cpu=999m
helm template test . --namespace=default --set foobar.app.resources.limits.cpu=null
```

You should end up with this output
```
⛵  docker-desktop in helm-testing/foobar2 on  main [✘!?]
❯ helm template test .
---
# Source: foobar2/charts/foobar/templates/test.yaml
resources:

  limits:
    cpu: 100m
    memory: 100Mi
  requests:
    cpu: 100m
    memory: 100Mi

⛵  docker-desktop in helm-testing/foobar2 on  main [✘!?]
❯ helm template test . --set foobar.app.resources.limits.cpu=999m
---
# Source: foobar2/charts/foobar/templates/test.yaml
resources:

  limits:
    cpu: 999m
    memory: 100Mi
  requests:
    cpu: 100m
    memory: 100Mi

⛵  docker-desktop in helm-testing/foobar2 on  main [✘!?]
❯ helm template test . --set foobar.app.resources.limits.cpu=null
---
# Source: foobar2/charts/foobar/templates/test.yaml
resources:

  limits:
    cpu: 100m
    memory: 100Mi
  requests:
    cpu: 100m
    memory: 100Mi


```

The problem is the last output should **NOT** have the field `resources.limits.cpu` set as Helm documentation says that `null` should remove a property, even if it is the default value.
