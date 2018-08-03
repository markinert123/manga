# manga
services:
  downloader:
    image: "bmzhao/kissmanga-downloader:latest"
    depends_on:
      - selenium
    environment:
      - SELENIUM_HOST=selenium
      - SELENIUM_PORT=24444
    volumes:
      - ./output:/output
    entrypoint:
      - java
      - -jar
      - /kissmanga-downloader.jar
      - http://kissmanga.com/Manga/Shingeki-no-Kyojin
  selenium:
    image: "elgalu/selenium:latest"
    ports:
      - "5900:25900"
    environment:
      - USE_SELENIUM=3
      - TZ=US/Pacific
      - VNC_PASSWORD=secret
    shm_size: 1g

#template-example: https://github.com/elgalu/docker-selenium/blob/master/docker-compose.yml
