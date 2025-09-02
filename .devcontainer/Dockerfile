# Pevně zamčená verze ESP-IDF
ARG DOCKER_TAG=v5.5
FROM espressif/idf:${DOCKER_TAG}

# Nastavení kódování
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# ===================================================================
#  RUČNÍ VYTVOŘENÍ UŽIVATELE 'vscode' (TOTO JE NOVÁ ČÁST)
# ===================================================================
# Aktualizace, instalace sudo a úklid
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends sudo

# Vytvoření uživatele vscode a přidání do sudo skupiny bez hesla
RUN useradd -ms /bin/bash vscode \
    && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# ===================================================================
#  Instalace našich nástrojů a další nastavení
# ===================================================================
# Aktualizace, instalace nástrojů a úklid v jednom kroku
RUN apt-get update -y \
    && apt-get install -y udev clang-format \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Automatické spuštění export.sh v terminálu pro nového uživatele 'vscode'
RUN echo "source /opt/esp/idf/export.sh > /dev/null 2>&1" >> /home/vscode/.bashrc

# Standardní příkazy pro spuštění
ENTRYPOINT [ "/opt/esp/entrypoint.sh" ]
CMD ["/bin/bash", "-c"]