# 1. Użyj oficjalnego obrazu agenta TeamCity jako bazy.
# Wybieramy wersję 'linux', która jest standardowym i wszechstronnym wyborem.
FROM jetbrains/teamcity-agent:latest

# 2. Przełącz się na użytkownika root, aby zainstalować oprogramowanie.
USER root

# 3. Ustaw zmienną środowiskową dla wersji Node.js (zalecana wersja LTS).
# Użycie zmiennej ułatwia aktualizację w przyszłości.
ENV NODE_VERSION=20.x

# 4. Zainstaluj podstawowe zależności oraz dodaj oficjalne repozytorium NodeSource.
# To rekomendowany sposób instalacji Node.js na systemach bazujących na Debianie/Ubuntu.
RUN apt-get update && \
    apt-get install -y curl gnupg && \
    curl -sL https://deb.nodesource.com/setup_${NODE_VERSION} | bash -

# Install dos2unix
RUN apt-get update && apt-get install -y dos2unix

# 5. Zainstaluj Node.js oraz, opcjonalnie, menedżer pakietów Yarn.
# Instalujemy również 'build-essential' na wypadek, gdyby niektóre pakiety npm
# wymagały kompilacji natywnych dodatków.
RUN apt-get install -y nodejs build-essential && \
    npm install -g yarn

RUN dos2unix /opt/buildagent/temp/agentTmp/docker-shell-script-*.sh

# 6. Wróć do domyślnego użytkownika 'buildagent', na którym pracuje agent TeamCity.
# To ważny krok ze względów bezpieczeństwa.
USER buildagent