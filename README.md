# KUTTL POC

This POC aims to understand how KUTTL works and what kind of tests we can do with kubernetes using this tool

## About Kuttl

KUTTL executes files in lexicographic order. The ordering matters
```
00-apply.yaml
00-assert.yaml
01-assert.yaml
```

### Apply vs Assert

`*-apply.yaml` files are applied to the cluster (same as `kubectl apply -f`) creating deployments, services, CRDs, pods, etc.

`*-assert.yaml` are checks, descriptions of the expected live resource.

KUTTL reads the live resource and compares whether the fields set in the assertion are present in the live resource.

After the apply step, KUTTL will make a polling to the cluster until assert matches or test timeout (defined in kuttl-test.yaml file) is reached. If the assertion never matches, step fails and test fails.

These tests are ran in an isolated namespace (it creates and teardown the namespace) so resources from different tests does not clash. This behavior can be overridden by specifying namespaces in manifests or test config.