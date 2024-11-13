# Base image
FROM mcr.microsoft.com/devcontainers/base:bullseye

# Argument for username
ARG USERNAME=vscode

# Set the DISPLAY environment variable
RUN echo "export DISPLAY=\$(grep nameserver /etc/resolv.conf | sed 's/nameserver //'):0" >> /etc/profile

# Used to persist bash history as per https://code.visualstudio.com/remote/advancedcontainers/persist-bash-history
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && mkdir /commandhistory \
    && touch /commandhistory/.bash_history \
    && chown -R $USERNAME /commandhistory \
    && echo "$SNIPPET" >> "/home/$USERNAME/.bashrc"

# Install jless (because it's not available at https://containers.dev/features at time of writing)
RUN NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
    && (echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/vscode/.profile \
    && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" \
    && brew install jless
