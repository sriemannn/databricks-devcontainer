FROM mcr.microsoft.com/devcontainers/base:resolute

ARG LOCAL_USER

RUN apt-get update && apt-get install -y \
  git python3-full python3-pip python3-setuptools \
  curl pipx build-essential zip \
  && rm -rf /var/lib/apt/lists/*

# Python virtual env setup
ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

WORKDIR /app

COPY . /app

RUN python3 -m pip install --no-cache-dir --upgrade pip
RUN python3 -m pip install -r requirements-dev.txt

# RUN pre-commit install --allow-missing-config

# RUN .venv/bin/python3 -m pip install pre-commit
# RUN ls .venv/bin

# RUN git config --system credentials.useHttpPath true \
#   && git config --system user.email "${@kaufland.com>LOCAL_USER}@kaufland.com" \
#   && git config --system user.name "${LOCAL_USER}"

# RUN .venv/bin/pre-commit install --allow-missing-config

ENV DATABRICKS_CONFIG_FILE="/app/.databrickscfg"
RUN curl -fsSL https://raw.githubusercontent.com/databricks/setup-cli/main/install.sh | sudo sh

# RUN echo "alias dab='databricks bundle'" >> ~/.bashrc \
  # && echo -e '#!/bin/bash\ndatabricks bundle "$@"' | sudo tee /usr/local/bin/dab >/dev/null \
  # && echo sudo chmod -x /usr/local/bin/dab

