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
    logger.go:42: 22:08:50 | config | Creating namespace: kuttl-test-liked-civet
=== NAME  kuttl/harness/unit
    logger.go:42: 22:08:50 | unit | Creating namespace: kuttl-test-mutual-crappie
=== NAME  kuttl/harness/integration
    logger.go:42: 22:08:50 | integration | Creating namespace: kuttl-test-enabling-tetra
=== NAME  kuttl/harness/unit
    logger.go:42: 22:08:50 | unit/0-apply | starting test step 0-apply
=== NAME  kuttl/harness/integration
    logger.go:42: 22:08:50 | integration/0-apply | starting test step 0-apply
=== NAME  kuttl/harness/config
    logger.go:42: 22:08:50 | config/0-apply | starting test step 0-apply
=== NAME  kuttl/harness/integration
    logger.go:42: 22:08:50 | integration/0-apply | Deployment:kuttl-test-enabling-tetra/web created
=== NAME  kuttl/harness/config
    logger.go:42: 22:08:50 | config/0-apply | Deployment:kuttl-test-liked-civet/web created
=== NAME  kuttl/harness/unit
    logger.go:42: 22:08:50 | unit/0-apply | Pod:kuttl-test-mutual-crappie/demo-pod created
=== NAME  kuttl/harness/config
    logger.go:42: 22:08:50 | config/0-apply | test step completed 0-apply
    logger.go:42: 22:08:50 | config | config events from ns kuttl-test-liked-civet:
=== NAME  kuttl/harness/integration
    logger.go:42: 22:08:50 | integration/0-apply | Service:kuttl-test-enabling-tetra/web-svc created
    logger.go:42: 22:08:50 | integration/0-apply | test step completed 0-apply
=== NAME  kuttl/harness/config
    logger.go:42: 22:08:50 | config | Deleting namespace: kuttl-test-liked-civet
=== NAME  kuttl/harness/integration
    logger.go:42: 22:08:50 | integration/1- | starting test step 1-
    logger.go:42: 22:08:51 | integration/1- | test step completed 1-
    logger.go:42: 22:08:51 | integration | integration events from ns kuttl-test-enabling-tetra:
    logger.go:42: 22:08:51 | integration | 2025-09-29 22:08:50 -0300 -03        Normal  Pod web-7f8f9d5f9d-k7lq7                Scheduled     Successfully assigned kuttl-test-enabling-tetra/web-7f8f9d5f9d-k7lq7 to minikube default-scheduler
    logger.go:42: 22:08:51 | integration | 2025-09-29 22:08:50 -0300 -03        Normal  ReplicaSet.apps web-7f8f9d5f9d          SuccessfulCreate       Created pod: web-7f8f9d5f9d-k7lq7       replicaset-controller
    logger.go:42: 22:08:51 | integration | 2025-09-29 22:08:50 -0300 -03        Normal  Deployment.apps web             ScalingReplicaSet     Scaled up replica set web-7f8f9d5f9d from 0 to 1 deployment-controller
    logger.go:42: 22:08:51 | integration | 2025-09-29 22:08:51 -0300 -03        Normal  Pod web-7f8f9d5f9d-k7lq7.spec.containers{nginx}       Pulled   Container image "nginx:1.25" already present on machine kubelet
    logger.go:42: 22:08:51 | integration | 2025-09-29 22:08:51 -0300 -03        Normal  Pod web-7f8f9d5f9d-k7lq7.spec.containers{nginx}       Created  Created container: nginx        kubelet
    logger.go:42: 22:08:51 | integration | 2025-09-29 22:08:51 -0300 -03        Normal  Pod web-7f8f9d5f9d-k7lq7.spec.containers{nginx}       Started  Started container nginx kubelet
    logger.go:42: 22:08:51 | integration | Deleting namespace: kuttl-test-enabling-tetra
=== NAME  kuttl/harness/unit
    logger.go:42: 22:08:52 | unit/0-apply | test step completed 0-apply
    logger.go:42: 22:08:52 | unit | unit events from ns kuttl-test-mutual-crappie:
    logger.go:42: 22:08:52 | unit | 2025-09-29 22:08:50 -0300 -03       Normal  Pod demo-pod            Scheduled       Successfully assigned kuttl-test-mutual-crappie/demo-pod to minikube   default-scheduler
    logger.go:42: 22:08:52 | unit | 2025-09-29 22:08:51 -0300 -03       Normal  Pod demo-pod.spec.containers{nginx}             Pulled  Container image "nginx:1.25" already present on machine        kubelet
    logger.go:42: 22:08:52 | unit | 2025-09-29 22:08:51 -0300 -03       Normal  Pod demo-pod.spec.containers{nginx}             Created Created container: nginx       kubelet
    logger.go:42: 22:08:52 | unit | 2025-09-29 22:08:51 -0300 -03       Normal  Pod demo-pod.spec.containers{nginx}             Started Started container nginx        kubelet
    logger.go:42: 22:08:52 | unit | Deleting namespace: kuttl-test-mutual-crappie
=== NAME  kuttl
    harness.go:403: run tests finished
    harness.go:510: cleaning up
    harness.go:567: removing temp folder: ""
--- PASS: kuttl (7.17s)
    --- PASS: kuttl/harness (0.00s)
        --- PASS: kuttl/harness/config (5.19s)
        --- PASS: kuttl/harness/integration (6.24s)
        --- PASS: kuttl/harness/unit (7.16s)
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