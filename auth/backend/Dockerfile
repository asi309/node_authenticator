FROM quay.io/keycloak/keycloak:22.0.5 as builder

# Enable health and metrics support
ENV KC_HEALTH_ENABLED=true
ENV KC_METRICS_ENABLED=true
# Enable GELF logging
ENV KC_LOG_LEVEL="INFO"
ENV KC_LOG="CONSOLE,GELF"
ENV KC_LOG_GELF_HOST="localhost"
ENV KC_LOG_GELF_PORT=12501
ENV KC_LOG_GELF_TIMESTAMP_FORMAT="'yyyy-MM-dd HH:mm:ss'"

# Configure a database vendor
ENV KC_DB=postgres

WORKDIR /opt/keycloak
RUN /opt/keycloak/bin/kc.sh build

FROM quay.io/keycloak/keycloak:22.0.5
COPY --from=builder /opt/keycloak/ /opt/keycloak/

# change these values to point to a running postgres instance
ENV KC_DB=keycloak
ENV KC_DB_URL=postgres
ENV KC_DB_USERNAME=keycloak
ENV KC_DB_PASSWORD=W0nder@1313
#ENV KC_HOSTNAME=localhost
ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start"]