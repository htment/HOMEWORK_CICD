FROM sonatype/nexus3:latest

# Установим OpenJDK
FROM openjdk:11-jre
RUN apt-get update && apt-get install -y --no-install-recommends util-linux && rm -rf /var/lib/apt/lists/*

# Создаем пользователя nexus
RUN groupadd -g 1000 nexus && useradd -u 1000 -g nexus -m -d /home/nexus -s /bin/bash nexus

# Создаем домашний каталог и устанавливаем права доступа.
RUN mkdir -p /home/nexus/.nexus && chown -R nexus:nexus /home/nexus/.nexus && chmod 700 /home/nexus/.nexus

# Копируем Nexus
COPY --from=sonatype/nexus3 /opt/sonatype/nexus /opt/sonatype/nexus

# Устанавливаем пользователя nexus по умолчанию.
USER nexus

# Команда для запуска Nexus
CMD ["/opt/sonatype/nexus/bin/nexus"]
