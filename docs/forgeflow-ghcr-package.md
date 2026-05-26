# Publishing the ForgeFlow Gitea image to GHCR

The fork publishes container images to GitHub Container Registry with the `publish-ghcr` workflow.

## Image names

The workflow publishes both the standard and rootless Gitea images:

```text
ghcr.io/scguoi/gitea:<tag>
ghcr.io/scguoi/gitea:<tag>-rootless
```

For the default branch, the workflow also publishes:

```text
ghcr.io/scguoi/gitea:latest
ghcr.io/scguoi/gitea:latest-rootless
```

## When images are published

Images are published when:

- commits are pushed to `main`;
- tags matching `v*` are pushed;
- the workflow is started manually from GitHub Actions.

## Required GitHub settings

The workflow uses the repository `GITHUB_TOKEN` and requires:

- Actions enabled for the repository;
- workflow permissions allowing package writes;
- package visibility configured as needed after the first publish.

No Docker Hub credentials are required.

The workflow publishes `linux/amd64` and `linux/arm64` images.

## Deployment example

```yaml
services:
  gitea:
    image: ghcr.io/scguoi/gitea:latest
    restart: unless-stopped
    ports:
      - "3000:3000"
      - "2222:22"
    volumes:
      - gitea-data:/data

volumes:
  gitea-data:
```
