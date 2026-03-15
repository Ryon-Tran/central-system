FROM odoo:18.0

# Install pip and OpenTelemetry dependencies
USER root
RUN apt-get update && \
    apt-get install -y python3-pip && \
    pip install --break-system-packages opentelemetry-distro opentelemetry-exporter-otlp opentelemetry-instrumentation-logging opentelemetry-instrumentation-requests opentelemetry-instrumentation-psycopg2 && \
    rm -rf /var/lib/apt/lists/*

USER odoo

# Entrypoint: run Odoo with OpenTelemetry instrumentation
CMD ["sh", "-c", "opentelemetry-instrument --traces_exporter otlp --service_name odoo --exporter_otlp_endpoint http://signoz-otel-collector:4317 --exporter_otlp_protocol grpc odoo -c /etc/odoo/odoo.conf"]
