# Update Bazel Docker container for new release

To build and publish docker container for new Bazel LTS release to `marketplace.gcr.io/google/bazel`, follow those steps:

## 1. Build the docker container on your local Linux machine

We need to first build and push the docker container to a staging repoistory `gcr.io/bazel-public/bazel`:
```bash
$ ./build.sh gcr.io/bazel-public/bazel <bazel version>
$ docker push gcr.io/bazel-public/bazel:<bazel version>
```
If the new Bazel version is the latest version (not a minor/patch release for previous major LTS version):
```bash
$ docker image list gcr.io/bazel-public/bazel:<bazel version>   # To check the <IMAGE ID>.
$ docker tag <IMAGE ID> gcr.io/bazel-public/bazel:latest
$ docker push gcr.io/bazel-public/bazel:latest
```

## 2. Submit the new version for review

We need to submit the new docker containers for review before it's available on the marketplace (`marketplace.gcr.io/google/bazel`).

- Open [the Bazel solution](https://pantheon.corp.google.com/partner/editor/click-to-deploy-containers/bazel?project=cloud-marketplace-ops) on Marketplace. If you don't have the permission, ping meteorcloudy@ for help.
- Click the `Edit` button of `VERSIONS`, then click the `Create Version` button to add the new version.
- Select the correct version tag and fill in the metadata (check other versions for examples).
- Click `Save` and then submit the new version for review.
