<!-- Warning: Do not manually edit this file. See notes on gluon + helm-docs at the end of this file for more information. -->
# istio-cni

![Version: 1.28.2-bb.0](https://img.shields.io/badge/Version-1.28.2--bb.0-informational?style=flat-square) ![AppVersion: 1.28.2](https://img.shields.io/badge/AppVersion-1.28.2-informational?style=flat-square) ![Maintenance Track: bb_integrated](https://img.shields.io/badge/Maintenance_Track-bb_integrated-green?style=flat-square)

Helm chart for istio-cni components

## Upstream References

- <https://github.com/istio/istio>

## Upstream Release Notes

- [Find upstream chart's release notes and CHANGELOG here](https://istio.io/latest/news/releases)

## Learn More

- [Application Overview](docs/overview.md)
- [Other Documentation](docs/)

## Pre-Requisites

- Kubernetes Cluster deployed
- Kubernetes config installed in `~/.kube/config`
- Helm installed

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

- Clone down the repository
- cd into directory

```bash
helm install istio-cni chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| upstream | object | Upstream chart values | Values to pass to [the upstream cni chart](https://github.com/istio/istio/blob/master/manifests/charts/istio-cni/values.yaml) |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.

---

_This file is programatically generated using `helm-docs` and some BigBang-specific templates. The `gluon` repository has [instructions for regenerating package READMEs](https://repo1.dso.mil/big-bang/product/packages/gluon/-/blob/master/docs/bb-package-readme.md)._

