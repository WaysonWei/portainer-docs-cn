# HonKit Documentation Project

This project uses HonKit to build and serve documentation. It includes Docker support and automated CI/CD with GitHub Actions.

## Local Development

### Prerequisites
- Node.js 18 or higher
- npm or yarn

### Setup
```bash
# Install dependencies
npm install

# Start development server with live reload
npm run dev

# Build static documentation
npm run build

# Serve built documentation
npm run serve
```

The development server will be available at `http://localhost:4000`.

## Docker

### Using Docker Compose (Recommended)
```bash
# Build and start the container
docker-compose up -d

# View logs
docker compose logs -f

# Stop the container
docker compose down

# Rebuild and restart
docker compose up -d --build
```

The documentation will be available at `http://localhost:8080`.

### Alternative: Manual Docker Commands
```bash
# Build the image
docker build -t honkit-docs .

# Run the container
docker run -p 8080:80 --name portainer-docs-cn honkit-docs
```

### Using Pre-built Image from Docker Hub
```bash
# Pull and run the published image
docker run -p 8080:80 --name portainer-docs-cn beos2020/portainer-docs-cn:latest

# Or modify docker-compose.yml to use the published image
# (see comments in docker-compose.yml file)
```

## GitHub Actions CI/CD

This project includes a GitHub Actions workflow that automatically builds and pushes Docker images to Docker Hub.

### Setup Requirements

1. **Docker Hub Account**: Create an account at [hub.docker.com](https://hub.docker.com)

2. **GitHub Secrets**: Add the following secrets to your GitHub repository:
   - `DOCKER_USERNAME`: Your Docker Hub username
   - `DOCKER_PASSWORD`: Your Docker Hub password or access token

### Setting up GitHub Secrets

1. Go to your GitHub repository
2. Click on **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add the following secrets:
   - Name: `DOCKER_USERNAME`, Value: your Docker Hub username
   - Name: `DOCKER_PASSWORD`, Value: your Docker Hub password

### Workflow Triggers

The workflow runs on:
- Push to `main` or `master` branch
- Push of version tags (e.g., `v1.0.0`)
- Pull requests to `main` or `master` branch

### Docker Image Tags

The workflow creates the following tags:
- `latest` (for main/master branch)
- Branch name (for branch pushes)
- Version tags (for semantic version tags like `v1.0.0`)
- PR number (for pull requests)

## Project Structure

```
.
├── cn/                 # Chinese documentation
├── en/                 # English documentation
├── _book/              # Built documentation (generated)
├── node_modules/       # Dependencies
├── .github/
│   └── workflows/
│       └── docker-build-push.yml  # CI/CD workflow
├── Dockerfile          # Docker build configuration
├── docker-compose.yml  # Docker Compose configuration
├── .dockerignore       # Docker ignore file
├── package.json        # Node.js dependencies and scripts
└── README.md          # This file
```

## Customization

### Nginx Configuration
To customize the nginx configuration, create an `nginx.conf` file and uncomment the line in the Dockerfile:
```dockerfile
COPY nginx.conf /etc/nginx/nginx.conf
```

### HonKit Configuration
Create a `book.json` file in the root directory to configure HonKit plugins and settings:
```json
{
  "title": "Documentation",
  "description": "Project documentation",
  "plugins": ["lunr", "search"],
  "pluginsConfig": {}
}
```

## Troubleshooting

### Build Issues
- Ensure all dependencies are installed: `npm install`
- Check Node.js version: `node --version` (should be 18+)
- Clear cache: `npm cache clean --force`

### Docker Issues
- Check Docker is running: `docker --version`
- Verify build context: ensure you're in the project root
- Check logs: `docker-compose logs` or `docker logs <container-id>`
- Rebuild containers: `docker-compose up -d --build`
- Reset everything: `docker-compose down && docker-compose up -d --build`

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test locally with `npm run dev`
5. Submit a pull request

The CI/CD pipeline will automatically build and test your changes.
