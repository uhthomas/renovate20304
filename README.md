# renovate20304

https://github.com/renovatebot/renovate/issues/20304

## Expected Behaviour

Renovate should replace the image `gcr.io/distroless/base-debian10` with `gcr.io/distroless/base-debian11:nonroot@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d`.

## Actual Behaviour

Renovate may perform the expected behaviour, but it will unexpectedly update the digest of `gcr.io/distroless/base-debian10` to the digest of `gcr.io/distroless/base-debian11:nonroot`.

```diff
-FROM gcr.io/distroless/base-debian10:debug
+FROM gcr.io/distroless/base-debian10:debug@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d
```

The above diff is incorrect and will not work.

```sh
❯ docker run gcr.io/distroless/base-debian10:debug@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d
Unable to find image 'gcr.io/distroless/base-debian10:debug@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d' locally
docker: Error response from daemon: manifest for gcr.io/distroless/base-debian10@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d not found: manifest unknown: Failed to fetch "sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d" from request "/v2/distroless/base-debian10/manifests/sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d".
See 'docker run --help'.
❯ docker run gcr.io/distroless/base-debian11:nonroot@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d
Unable to find image 'gcr.io/distroless/base-debian11:nonroot@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d' locally
gcr.io/distroless/base-debian11@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d: Pulling from distroless/base-debian11
5f80a38cb015: Pull complete 
9fb3436fe506: Pull complete 
4f70717a8bb3: Pull complete 
Digest: sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d
Status: Downloaded newer image for gcr.io/distroless/base-debian11@sha256:5f1e20553a35537925dafe9b6a4d6805deecfbb76c2e419ef72d9023166ec09d
```
