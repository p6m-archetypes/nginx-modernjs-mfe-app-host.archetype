# {{ project-title }}

An nginx-based micro frontend host designed to serve and orchestrate multiple pre-built Modern.js micro frontend applications.

## Getting Started

### Prerequisites

- Docker (for containerized deployment)

### Local Development

Build and run the Docker container:

```bash
# Build the image
docker build -t {{ project-name }} .

# Run the container
docker run -p {{ port }}:{{ port }} {{ project-name }}
```

The application will be available at http://localhost:{{ port }}/apps/

### Production Deployment

This host is designed to serve pre-built micro frontend applications. There's no build step required for the host itself.

## Micro Frontend Architecture

This nginx host serves static micro frontend applications with optimized CORS headers and caching for production use.

### Adding Micro Frontend Applications

To deploy a micro frontend to this host:

1. **Build your micro frontend**: 
   ```bash
   # In your Modern.js micro frontend project
   pnpm build
   ```

2. **Copy to apps directory**:
   ```bash
   # Copy the dist output to the host
   cp -r dist/ /path/to/host/{{ apps-dir }}/your-app-name/
   ```

3. **Access your application**:
   - Your app will be available at: `http://host/{{ apps-dir }}/your-app-name/`

### Directory Structure

```
{{ apps-dir }}/
├── app1/           # First micro frontend
│   ├── index.html
│   ├── assets/
│   └── ...
├── app2/           # Second micro frontend  
│   ├── index.html
│   ├── assets/
│   └── ...
└── index.html      # Optional host landing page
```

### CORS Configuration

The nginx configuration includes CORS headers to support:
- Cross-origin requests between micro frontends
- Module Federation remote loading
- Dynamic asset loading

### Nginx Configuration

The included `nginx.conf` provides:
- Static file serving with proper MIME types
- CORS headers for micro frontend communication
- Optimized caching for static assets
- Fallback routing for single-page applications

## Docker Deployment

The multi-stage Dockerfile builds a lightweight nginx container:

```bash
# Build image
docker build -t {{ project-name }} .

# Run container  
docker run -p {{ port }}:{{ port }} {{ project-name }}
```

The container:
- Uses `nginx:alpine` for minimal size
- Copies apps directory to `/usr/share/nginx/html/{{ apps-dir }}/`
- Configures nginx with custom `nginx.conf`
- Exposes port {{ port }}

## Kubernetes Deployment

Deploy to Kubernetes using the included manifests:

```bash
# Apply the Kubernetes configuration
kubectl apply -f .platform/kubernetes/base/
```

The Kubernetes deployment includes:
- Service configuration for load balancing
- Ingress configuration for external access
- Health check endpoints
- Resource limits and requests
