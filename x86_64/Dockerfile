FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG TZ=Australia/Melbourne

RUN apt-get update && apt-get install -y apt-transport-https software-properties-common tzdata wget apt-utils gnupg2 curl sudo && \
    install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
    chmod a+r /etc/apt/keyrings/docker.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    wget -qO- https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/dart.gpg && \
    echo 'deb [signed-by=/usr/share/keyrings/dart.gpg arch=amd64] https://storage.googleapis.com/download.dartlang.org/linux/debian stable main' | sudo tee /etc/apt/sources.list.d/dart_stable.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
    wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
    https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
    tee /etc/apt/sources.list.d/hashicorp.list && \
    echo \
    "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb" && \
    dpkg -i packages-microsoft-prod.deb && \
    rm packages-microsoft-prod.deb

RUN apt-get update \
    && apt-get install -y \
    aria2 \
    busybox \
    cloc \
    dart \
    dnsutils \
    docker-ce docker-ce-cli containerd.io \
    dotnet-sdk-8.0 \
    exa \
    git \
    golang \
    google-cloud-cli \
    htop \
    imagemagick \
    jq \
    mc \
    mysql-client \
    ncdu \
    nmap \
    nodejs npm \
    openjdk-11-jdk \
    openssh-client \
    php php-cli php-cgi php-mysql php-pgsql \
    postgresql-client \
    powershell \
    python3 python3-pip \
    rclone \
    screen \
    terraform \
    time \
    tmux \
    vim \
    wget \
    zsh \
    && curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash \
    && curl -fsSL https://d2lang.com/install.sh | sh -s -- \
    && rm -rf /var/lib/apt/lists/* \
    && curl -sSL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -bfp /usr/local && \
    rm -rf /tmp/miniconda.sh && \
    wget https://dlcdn.apache.org/maven/maven-3/3.9.8/binaries/apache-maven-3.9.8-bin.tar.gz && \
    tar -xvf apache-maven-3.9.8-bin.tar.gz && \
    mv apache-maven-3.9.8 /opt/ && \
    rm -rf apache-maven-3.9.8-bin.tar.gz && \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y && \
    apt-get clean

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -rf ./aws && rm awscliv2.zip

# Install AZ Copy
RUN wget "https://aka.ms/downloadazcopy-v10-linux" -O azcopy.tar.gz && \
    tar -xf azcopy.tar.gz && \
    mv azcopy_linux_amd64_*/azcopy /usr/local/bin/ && \
    rm -rf azcopy_linux_amd64_* && rm azcopy.tar.gz

# Install kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

ARG USER=coder
RUN useradd --groups sudo,docker --no-create-home --shell /usr/bin/zsh ${USER} \
    && echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
    && chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}

RUN echo 'M2_HOME=/opt/apache-maven-3.9.8' >> ~/.zshrc && \
    echo 'PATH="$M2_HOME/bin:$PATH:/usr/lib/dart/bin"' >> ~/.zshrc \
    echo 'alias la="ls -la"' >> ~/.zshrc && \
    echo 'alias tf=terraform' >> ~/.zshrc && \
    echo 'alias k=kubectl' >> ~/.zshrc && \
    echo 'alias kga="kubectl get all"' >> ~/.zshrc && \
    echo 'alias kgn="kubectl get nodes"' >> ~/.zshrc && \
    echo 'alias kgs="kubectl get svc"' >> ~/.zshrc && \
    echo 'alias kgp="kubectl get pods"' >> ~/.zshrc && \
    echo 'alias kgd="kubectl get deploy"' >> ~/.zshrc && \
    echo 'alias kgcm="kubectl get cm"' >> ~/.zshrc && \
    echo 'alias kgsec="kubectl get secret"' >> ~/.zshrc && \
    echo 'alias kgns="kubectl get ns"' >> ~/.zshrc
