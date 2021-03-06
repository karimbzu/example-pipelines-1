# example-pipelines

Example Tekton Trigger pipelines/resources

## Compatibility

The master branch of this repo, should work with the master branch of webhooks-extension.  If not running on master, then you should find branches available in this repository named at the levels of dashboard/webhooks-extension they support.

## Pipelines
- `simple-pipeline`

This pipeline expects the headers from a GitHub webhook event to be stored as JSON within the `event-headers` param.
This pipeline builds the Dockerfile specified within the GitHub repository and pushes to the image to the specified registry.
Afterwards, and only on push events, `kubectl apply -f config` will run against the GitHub repository.

- `simple-manual-pipeline`

This pipeline is the same as the `simple-pipeline` pipeline, but does not take any parameters or gate deployment depending on event type.
This makes it easy to rebuild.

- `simple-buildah-pipeline`

This pipeline is the same as the `simple-manual-pipeline` pipeline, but uses the `buildah` image to build and push the Dockerfile instead of using Docker.
This pipeline requires `buildah` task from https://github.com/tektoncd/catalog/blob/master/buildah/buildah.yaml.