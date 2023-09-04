FROM ubuntu

RUN apt-get update && apt-get install -y apt-transport-https software-properties-common wget apt-utils gnupg2 curl sudo && \
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
        dart \
        docker-ce docker-ce-cli containerd.io \
        dotnet-sdk-7.0 \
        cloc \
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
        powershell \
        postgresql-client \
        python3 python3-pip \
        rclone \
        terraform \
        tmux \
        vim \
        wget \
        zsh \
        && curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash \
        && rm -rf /var/lib/apt/lists/* \
        && curl -sSL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -bfp /usr/local && \
    rm -rf /tmp/miniconda.sh && \
	wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz && \
	tar -xvf apache-maven-3.6.3-bin.tar.gz && \
	mv apache-maven-3.6.3 /opt/ && \
    rm -rf apache-maven-3.6.3-bin.tar.gz && \
    apt-get clean

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -rf ./aws && rm awscliv2.zip

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Australia/Melbourne

ARG USER=coder
RUN useradd --groups sudo,docker --no-create-home --shell /usr/bin/zsh ${USER} \
        && echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
        && chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}

RUN echo 'M2_HOME=/opt/apache-maven-3.6.3' >> ~/.zshrc && \
    echo 'PATH="$M2_HOME/bin:$PATH"' >> ~/.zshrc