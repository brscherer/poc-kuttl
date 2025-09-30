# KUTTL POC

This POC aims to understand how KUTTL works and what kind of tests we can do with kubernetes using this tool

## How to Run

Clone this repo and enter in the repo folder, run:

`kubectl kuttl test --config kuttl-test.yaml`

### Output

```bash
% kubectl kuttl test --config kuttl-test.yaml
=== RUN   kuttl
    harness.go:459: starting setup
    harness.go:254: running tests using configured kubeconfig.
    harness.go:277: Successful connection to cluster at: https://127.0.0.1:52109
    harness.go:362: running tests
    harness.go:74: going to run test suite with timeout of 30 seconds for each step
    harness.go:374: testsuite: ./tests has 3 tests
=== RUN   kuttl/harness
=== RUN   kuttl/harness/config
=== PAUSE kuttl/harness/config
=== RUN   kuttl/harness/integration
=== PAUSE kuttl/harness/integration
=== RUN   kuttl/harness/unit
=== PAUSE kuttl/harness/unit
=== CONT  kuttl/harness/config
=== CONT  kuttl/harness/unit
=== CONT  kuttl/harness/integration
=== NAME  kuttl/harness/config
    logger.go:42: 22:02:42 | config | Ignoring deployment-check as it does not match file name regexp: ^(\d+)-(?:[^\.]+)(?:\.yaml)?$
=== NAME  kuttl/harness/integration
    logger.go:42: 22:02:42 | integration | Ignoring web-app as it does not match file name regexp: ^(\d+)-(?:[^\.]+)(?:\.yaml)?$
=== NAME  kuttl/harness/unit
    logger.go:42: 22:02:42 | unit | Ignoring pod-basic as it does not match file name regexp: ^(\d+)-(?:[^\.]+)(?:\.yaml)?$
=== NAME  kuttl/harness/config
    logger.go:42: 22:02:42 | config | Creating namespace: kuttl-test-moral-locust
=== NAME  kuttl/harness/unit
    logger.go:42: 22:02:42 | unit | Creating namespace: kuttl-test-apt-serval
=== NAME  kuttl/harness/integration
    logger.go:42: 22:02:42 | integration | Creating namespace: kuttl-test-polished-rhino
    logger.go:42: 22:02:42 | integration | integration events from ns kuttl-test-polished-rhino:
=== NAME  kuttl/harness/unit
    logger.go:42: 22:02:42 | unit | unit events from ns kuttl-test-apt-serval:
=== NAME  kuttl/harness/config
    logger.go:42: 22:02:42 | config | config events from ns kuttl-test-moral-locust:
    logger.go:42: 22:02:42 | config | Deleting namespace: kuttl-test-moral-locust
=== NAME  kuttl/harness/unit
    logger.go:42: 22:02:42 | unit | Deleting namespace: kuttl-test-apt-serval
=== NAME  kuttl/harness/integration
    logger.go:42: 22:02:42 | integration | Deleting namespace: kuttl-test-polished-rhino
=== NAME  kuttl
    harness.go:403: run tests finished
    harness.go:510: cleaning up
    harness.go:567: removing temp folder: ""
--- PASS: kuttl (5.23s)
    --- PASS: kuttl/harness (0.00s)
        --- PASS: kuttl/harness/config (5.11s)
        --- PASS: kuttl/harness/integration (5.16s)
        --- PASS: kuttl/harness/unit (5.21s)
PASS
```

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