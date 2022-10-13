### Sentry charts

This repository contains the sentry and clickhouse charts that is cloned from https://github.com/sentry-kubernetes/charts/tree/16.0.0 wherein 16.0.0 is the latest released tag in the upstream repo at the time of writing this commit.


## Changes made to run in MAC M1 machines
- Changed docker image and tag for `clickhouse` and `redis` to run in Mac M1. Please extact the `.tgz` files to know the changes. Changed some data related to `replicas` to suit the RAM of my local mac.
- Changed `clickhouse` to run as `single` node and not as cluster as there was some issue wrt Zookeeper when runnning in cluster mode. Refer `sentry/templates/configmap-snuba.yaml` for the settings.
- Increased `activeDeadlineSeconds` for `hooks` as the dependcies take much time to come online. Refer `hooks` section under `sentry/values.yaml`
- Changed nginx type from `ClusterIP` to `NodePort` so that we can access the sentry-web in local at `localhost:<nodeport>`. Refer `nginx` section under `sentry/values.yaml`
