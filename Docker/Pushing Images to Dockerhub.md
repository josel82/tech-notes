```bash
# Create a builder if you haven't already
docker buildx create --name multiarch-builder --use

# Build and push for both AMD64 and ARM64
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t username/image_name:latest \
  -t username/image_name:v1.0.0 \
  --push .

```