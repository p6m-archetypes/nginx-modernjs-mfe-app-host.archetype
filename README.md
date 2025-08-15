# Nginx Modern.js MFE Host Archetype

![Latest Release](https://img.shields.io/github/v/release/p6m-archetypes/nginx-modernjs-mfe-app-host.archetype?style=flat-square&label=Latest%20Release&color=blue)

This is an [Archetect](https://archetect.github.io/) archetype for building nginx-based micro frontend (MFE) host applications that serve static Modern.js applications on Kubernetes.

## Features

- **Nginx-Based Host**: Lightweight nginx server optimized for serving static micro frontend applications
- **CORS Ready**: Pre-configured CORS headers for seamless micro frontend integration
- **Static File Serving**: Optimized nginx configuration for serving built Modern.js applications
- **Docker Ready**: Includes optimized multi-stage Dockerfile with nginx:alpine for minimal container size
- **Kubernetes Compatible**: Configured for seamless deployment on Kubernetes clusters with proper health checks
- **Apps Directory**: Dedicated `/apps/` directory structure for hosting multiple micro frontend builds
- **Production Optimized**: Nginx configuration tuned for production performance and caching
- **Zero Dependencies**: No Node.js runtime dependencies - pure static file serving

## Usage

Generate a new project from this archetype:

```sh
archetect render git@github.com:p6m-archetypes/nginx-modernjs-mfe-app-host.archetype.git
```

This creates an nginx-based MFE host ready to:
- Serve multiple pre-built micro frontend applications
- Handle CORS requests for cross-origin micro frontend communication
- Deploy to Kubernetes clusters with minimal resource footprint
- Run as a lightweight Docker container

## Getting Started

After generating your project:

1. **Build the Docker image**: `docker build -t your-mfe-host .`
2. **Run the container**: `docker run -p 80:80 your-mfe-host`
3. **Access your host**: `http://localhost/apps/`
4. **Deploy micro frontends**: Place built applications in the `/apps/` directory
5. **Deploy to Kubernetes**: Use the included manifests in `.platform/kubernetes/`

## Deploying Micro Frontends

To add a micro frontend application:

1. Build your Modern.js application: `pnpm build`
2. Copy the `dist/` output to the host's `apps/your-app-name/` directory
3. Access your app at: `http://your-host/apps/your-app-name/`

The nginx configuration automatically serves all content with proper CORS headers for micro frontend integration.
