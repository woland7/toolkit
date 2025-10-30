# Use Debian Bookworm as the base image
FROM debian:bookworm

# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    curl \
    gnupg
RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com bookworm main" > /etc/apt/sources.list.d/hashicorp.list

# Install system dependencies
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    unzip \
    git \
    sudo \
    openssl \
    openjdk-17-jdk \
    ca-certificates \
    terraform \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Python tools
RUN pip3 install --no-cache-dir --break-system-packages \
    ansible \
    ansible-lint \
    yamllint \
    jsonlint \
    black \
    checkov

RUN ansible-galaxy collection install oracle.oci

# Set environment variables
ARG TERRAGRUNT_VERSION=v0.56.3

# ----------------------------
# Install TFLint
# ----------------------------
# ----------------------------
# Install TFLint (fixed)
# ----------------------------
RUN curl -s https://raw.githubusercontent.com/terraform-linters/tflint/master/install_linux.sh | bash


# ----------------------------
# Install Terragrunt
# ----------------------------
#RUN curl -L "https://github.com/gruntwork-io/terragrunt/releases/download/${TERRAGRUNT_VERSION}/terragrunt_linux_amd64" -o /usr/local/bin/terragrunt && \
#    chmod +x /usr/local/bin/terragrunt

# ----------------------------
# Install Terrascan
# ----------------------------
#RUN curl -s https://api.github.com/repos/tenable/terrascan/releases/latest \
#    | grep -o -E "https://.+?_Linux_x86_64.tar.gz" \
#    | head -n 1 \
#    | xargs curl -L -o terrascan.tar.gz && \
#    tar -xf terrascan.tar.gz terrascan && \
#    install terrascan /usr/local/bin/terrascan && \
#    rm terrascan terrascan.tar.gz


# Install Terraform (latest version)
# Add HashiCorp GPG key and repo

RUN apt-get update && apt-get install -y wget && \
    wget -O /opt/Insomnia.Core-11.6.2.exe \
    https://github.com/Kong/insomnia/releases/download/core%4011.6.2/Insomnia.Core-11.6.2.exe && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Set default command
CMD ["/bin/bash"]