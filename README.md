# hello-nextjs

A [Next.js](https://nextjs.org/) application, containerized with Docker and deployed to a Kubernetes cluster on the [Section](https://www.section.io/) edge platform via GitHub Actions.

## Tech Stack

- [Next.js](https://nextjs.org/) 13
- [React](https://react.dev/) 18
- [Tailwind CSS](https://tailwindcss.com/) (via CDN, see `public/index.html`)

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- npm

### Install dependencies

```bash
npm install
```

### Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to view the app.

### Build for production

```bash
npm run build
npm run start
```

## Project Structure

```
pages/            Next.js pages (App component in _app.js)
public/           Static assets, including the app's index.html
next.config.js    Next.js configuration (rewrites/redirects)
Dockerfile        Multi-stage build for a production container image
ci/deploy.sh       Deployment script used by CI to roll out to Kubernetes
k8s/              Kubernetes manifests (Deployment, Ingress)
```

## Docker

Build and run the production image locally:

```bash
docker build -t hello-nextjs .
docker run -p 3000:3000 hello-nextjs
```

## Deployment

Pushes to `main` trigger the [`Deploy to Section`](.github/workflows/workflows.yaml) GitHub Actions workflow, which:

1. Builds the Docker image and pushes it to the GitHub Container Registry (`ghcr.io`).
2. Applies the Kubernetes manifests in `k8s/` and rolls out the new image via `ci/deploy.sh`.

The cluster this deploys to is hosted on [Section](https://www.section.io/). See the [Section documentation](https://www.section.io/docs/) for details on managing domains, locations, and providers for the underlying platform.

## Get Involved

Join the Section Discord community to get help from their team and other developers.

[![Discord](https://img.shields.io/discord/554724688312401921?color=7289da&label=discord&logo=discord&logoColor=white)](https://discord.gg/J7fUts7j)
[![Twitter](https://img.shields.io/twitter/follow/sectionio?style=social)](https://twitter.com/sectionio)
