# Security exceptions

## restaurant-template legacy image

**Image:** `ghcr.io/linkmush/restaurant-template:1.1`

**Affected environments:**

- `restaurant-dev`
- `restaurant-prod`

**Detected issues:**

- Container runs as UID `0` (root).
- Image has not been verified with a read-only root filesystem.

**Temporary KubeLinter exceptions:**

- `run-as-non-root`
- `no-read-only-root-fs`

**Reason:**

The existing application image is treated as an externally delivered
legacy image. The platform configuration must not force an arbitrary
user ID or a read-only root filesystem without confirming that the image
supports those settings.

**Required remediation:**

The application/image owner must provide a new image that:

- runs as a non-root user;
- supports `runAsNonRoot: true`;
- supports `readOnlyRootFilesystem: true`;
- uses writable volumes only for required paths.

When a compliant image is available, remove the exceptions from
`.kube-linter.yaml`.