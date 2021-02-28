# oc CLI Cheat Sheet

Below is a list of sample `oc` commands to help you through some of the labs

## Login/User management

`oc login`   - authenticate to an openshift cluster

`oc logout`  - end the current session

`oc whoami`  - show the current user context

## Project management

`oc project`     - show the current project context

`oc new-project` - create a new project in Openshift and change to that context

## Resource management

`oc new-app [RESOURCE]`           - create a new application from from source code, container image, or OpenShift template

`oc new-build [SOURCE]`           - create a new build configuration from source code

`oc label [RESOURCE] [KEY=VALUE]` - add/update/remove labels from an Openshift resource

`oc create -f [FILE]`             - create a new resource from filename or stdin

`oc get [RESOURCE]`               - retrieve a resource (use -o for additional output options)

`oc replace`                      - replace an existing resource from filename or stdin

`oc delete [RESOURCE]`            - delete a resource

`oc edit [RESOURCE]`              - modify a resource from text editor

`oc describe [RESOURCE]`          - retrieve a resource with details

## Cluster management

`oc adm policy`                - manage role/scc to user/group bindings, as well as additional policy administration

`oc adm cordon/uncordon/drain` - unschedule/schedule/drain a node

## Additional resource management

`oc patch [RESOURCE]`    - Update fields for a resource with JSON or YAML segments

`oc extract [RESOURCE]`  - get configmaps or secrets and save to disk

`oc set env`             - set environment variables on a pod template/deployment configuration/build configuration

`oc set image`           - update the image for deployment configurations/daemonsets

## Operational commands

`oc logs`       - retrieve the logs for a resource (build configurations,deployment configurations, and pods)

`oc rsh [POD]`  - remote shell into a container

`oc rsync`      - copy files to or from a container

`oc exec`       - execute a command in a container

`oc run`        - create a deployment configuration from image

`oc idle`       - scale resources to zero replicas


## Build / Deploy

`oc rollout`        - manage deployments from deployment configuration

`oc rollout latest` - start a new deployment with the latest state

`oc rollout undo`   - perform a rollback operation

`oc rollout status` - watch the status of a rollout until complete

`oc start-build`    - start a new build from a build configuration

`oc cancel-build`   - cancel a build in progress

`oc import-image`   - pull in images and tags from an external Docker registry

`oc scale`          - change the number of pod replicas for a deployment