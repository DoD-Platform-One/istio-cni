# Developer Maintenance

## Istio CNI Overview

This package is optional when using Istio in sidecar mode and required when using with Ambient.

## How to upgrade the Istio CNI Package chart

`istio-cni` is a passthrough chart. That means it does not fork an upstream
chart but instead embeds one as a dependency. Because of this, the upgrade
process is incredibly simple.

1. Checkout the branch that renovate created. This branch will have the image
   tag updates and typically some other necessary version changes that you will
   want. You can either work off of this branch or branch off of it.

1. Update dependency archives via `helm` (from repository root)
   ```sh
   helm dependency update ./chart
   ```

1. Update version references for the chart in `Chart.yaml`. `version` should be
   `<version>-bb.0` (ex: `1.25.1-bb.0`) and `appVersion` should be `<version>`
   (ex: `1.25.1`). Also validate that the Big Bang
   `bigbang.dev/applicationVersions` and `helm.sh/images` annotations are update
   to reflect the chart's new application and image versions.

1. Add an entry to `CHANGELOG.md` detailing what changed in the update. At a
   minimum mention updating the dependency chart.

1. Regenerate the readme following the
   [steps in Gluon](https://repo1.dso.mil/platform-one/big-bang/apps/library-charts/gluon/-/blob/master/docs/bb-package-readme.md).

1. Open an MR (or check the one that Renovate created for you) and validate that
   the pipeline is successful.

1. Follow the testing steps below for some manual confirmations.

## Testing new Istio CNI version

When building your development cluster add in the additional values file from `tests\test-values.yaml` to the end of your helm command.  You can verify the package is working as expected by executing the following command:

```sh
kubectl get pods -A -o jsonpath='{.items[*].spec.initContainers[*].name}' | grep istio-validation
```

The cni negates the need for the `istio-init` initContainer which results in each istio injected workload having an initContainer of `istio-validation` instead.  You can double check this by executing the following command to verify there are no references of `istio-init`:

```sh
kubectl get pods -A -o jsonpath='{.items[*].spec.initContainers[*].name}' | grep istio-init
```

> **Note**: There is currently [an issue](https://github.com/istio/istio/pull/57110) that may come up during the development process.
> Typically the value for `istioCNI.values.upstream.global.platform` should be set to `k3d` for K3d/Rancher clusters. 
> Due to the referenced issue it is currently set to `k3s`.  It's possible this may change once the referenced issue is fixed so the test-values will need to be adjusted accordingly.

## Big Bang MR Guidance

Once the upgrade MR has been approved a new version will be cut and an MR will be opened on the Big Bang repository.  Since this package follows the same versioning as `istio-crds`, `istiod`, and `istio-gateway`, it is recommended to close all but one of the Big Bang MR's and use the consolidated MR to update all versions.