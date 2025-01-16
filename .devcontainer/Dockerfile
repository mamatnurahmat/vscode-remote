# Use a base Python image with Debian for better compatibility
FROM python:3.12-slim

# Install Docker CLI and other dependencies for Docker-in-Docker
RUN apt-get update && apt-get install -y \
    docker.io \
    docker-compose-plugin \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Optional: Set up a non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && usermod -aG docker $USERNAME

# Switch to non-root user for better security
USER $USERNAME

# Set the working directory
WORKDIR /workspace

# Copy requirements and install dependencies
COPY ../requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Set default command
CMD ["python3"]
