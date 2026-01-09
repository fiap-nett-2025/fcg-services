FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app
EXPOSE 8080
EXPOSE 8081

# Variáveis do agente
ENV CORECLR_ENABLE_PROFILING=1 \
    CORECLR_PROFILER={36032161-FFC0-4B61-B559-F6C5D41BAE5A} \
    CORECLR_NEWRELIC_HOME=/usr/local/newrelic-dotnet-agent \
    CORECLR_PROFILER_PATH=/usr/local/newrelic-dotnet-agent/libNewRelicProfiler.so

USER root

RUN apt-get update && \
    apt-get install -y wget ca-certificates gnupg && \
    mkdir -p /usr/share/keyrings && \
    wget -O- https://download.newrelic.com/548C16BF.gpg | gpg --dearmor -o /usr/share/keyrings/newrelic-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/newrelic-archive-keyring.gpg] http://apt.newrelic.com/debian/ newrelic non-free" > /etc/apt/sources.list.d/newrelic.list && \
    apt-get update && \
    apt-get install -y newrelic-dotnet-agent && \
    rm -rf /var/lib/apt/lists/*

# USER $APP_UID

CMD ["dotnet", "app.dll"]
