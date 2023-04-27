FROM python:3.10.7-slim-buster

#RUN useradd app

EXPOSE 80

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PORT=80

WORKDIR /app
#COPY --chown=app:app . .

RUN apt-get update --yes --quiet

# deps used by Chrome et Selenium
RUN apt-get install --yes --quiet --no-install-recommends \
    gettext \
    fonts-liberation \
    libasound2 \
    libatk-bridge2.0-0 \
    libatk1.0-0 \
    libatspi2.0-0 \
    libcairo2 \
    libcups2 \
    libcurl3-gnutls \
    libcurl3-nss \
    libcurl4 \
    libdbus-1-3 \
    libdrm2 \
    libgbm1 \
    libgdk-pixbuf2.0-0 \
    libglib2.0-0 \
    libgtk-3-0 \
    libnspr4 \
    libnss3 \
    libpango-1.0-0 \
    libu2f-udev \
    libvulkan1 \
    libx11-6 \
    libxcb1 \
    libxcomposite1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxkbcommon0 \
    libxrandr2 \
    libxshmfence1 \
    wget \
    xdg-utils \
    netcat \
    xvfb \
 && rm -rf /var/lib/apt/lists/*

COPY ../../testpgbouncer ./testpgbouncer
COPY ../../templates ./templates
COPY ../../manage.py .
COPY ../../requirements.txt .

RUN pip install "daphne==3.0.2"
RUN pip install -r requirements.txt

#USER app

CMD set -xe; daphne -b 0.0.0.0 -p 80 testpgbouncer.asgi:application
