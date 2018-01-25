# How to submit conformance results

## The tests

The standard set of conformance tests is currently those defined by the
`[Conformance]` tag in the
[kubernetes e2e](https://github.com/kubernetes/kubernetes/tree/master/test/e2e)
suite.

## Running

The standard tool for running these tests is
[Sonobuoy](https://github.com/heptio/sonobuoy), and the standard way to run
these in your cluster is with `curl -L https://raw.githubusercontent.com/cncf/k8s-conformance/master/sonobuoy-conformance.yaml | kubectl apply -f -`.

Watch Sonobuoy's logs with `kubectl logs -f -n sonobuoy sonobuoy` and wait for
the line `no-exit was specified, sonobuoy is now blocking`.  At this point, use
`kubectl cp` to bring the results to your local machine, expand the tarball, and
retain the 2 files `plugins/e2e/results/{e2e.log,junit.xml}`, which will
be included in your submission.

The last file to include in your submission can be obtained by executing 
`kubectl version > version.txt`. 

## Uploading

Prepare a PR to
[https://github.com/cncf/k8s-conformance](https://github.com/cncf/k8s-conformance).
In the descriptions below, `X.Y` refers to the kubernetes major and minor
version, and `$dir` is a short subdirectory name to hold the results for your
product.  Examples would be `gke` or `openshift`.

Description: `Conformance results for vX.Y/$dir`

### Contents of the PR

```
vX.Y/$dir/README.md: A script or human-readable description of how to reproduce
your results.
vX.Y/$dir/version.txt: Test and cluster versions (from Sonobuoy).
vX.Y/$dir/e2e.log: Test log output (from Sonobuoy).
vX.Y/$dir/junit_01.xml: Machine-readable test log (from Sonobuoy).
vX.Y/$dir/PRODUCT.yaml: See below.
```

#### PRODUCT.yaml

This file describes your product. It is YAML formatted with the following root-level fields. Please fill in as appropriate.

| Field               | Description |
| ------------------- | ----------- |
| `vendor`            | Name of the legal entity that is certifying. This entity must have a signed participation form on file with the CNCF  |
| `name`              | Name of the product being certified. |
| `version`           | The version of the product being certified (not the version of Kubernetes it runs). |
| `website_url`       | URL to the product information website |
| `documentation_url` | URL to the product documentation |
| `product_logo_url`  | URL to the product's logo, prefrably in SVG format. OPTIONAL. If not supplied, your product will not be listed on any Kubernetes/CNCF marketing around conformance |

Examples below are for a fictional Kubernetes implementation called _Turbo
Encabulator_ produced by a company named _Yoyodyne_.

```yaml
vendor: Yoyodyne
name: Turbo Encabulator
version: v1.7.4
website_url: https://yoyo.dyne/turbo-encabulator
documentation_url: https://yoyo.dyne/turbo-encabulator/docs
product_logo_url: https://yoyo.dyne/assets/turbo-encabulator.svg
```

### Sample PR

See https://github.com/mml/k8s-conformance/pull/1 for a sample.

## Amendment for Private Review

If you need a private review for an unreleased product, please contact conformance@cncf.io.
Note that your results must be made public at launch, at the time you start using the
Certified Kubernetes Marks.

## Review

A reviewer will shortly comment on and/or accept your pull request, following this [process](reviewing.md).
If you don't see a response within 3 business days, please contact conformance@cncf.io.

## Issues

If you have problems certifying that you feel are an issue with the conformance
program itself (and not just your own implementation), you can file an issue in
the [repository](https://github.com/cncf/k8s-conformance). Questions and
comments can also be sent to the working group's 
[mailing list and slack channel](README-WG.md).
[SIG Architecture](https://github.com/kubernetes/community/tree/master/sig-architecture)
is the change controller of the conformance definition. We track a
[list of issue resolutions](https://github.com/cncf/k8s-conformance/issues/27) with SIG Architecture.
