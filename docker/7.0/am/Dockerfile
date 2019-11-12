FROM gcr.io/forgerock-io/am:7.0.0-b33f5b14758a42cfc02c2e36b084955d5453bc74

# BEGIN - temporary work around for testing if the ds-idrepo is configured before AM starts. Remove when FBC is integrated
# Installs ldap utils for querying the repo.
USER root
RUN apt-get update && apt-get install -y ldap-utils
USER forgerock
COPY --chown=forgerock:root openam /home/forgerock/openam
# END

COPY logback.xml /usr/local/tomcat/webapps/am/WEB-INF/classes


# This copies in the boot.json and other files...
COPY --chown=forgerock:root openam /home/forgerock/openam

# Override the entrypoint and just start tomcat
#CMD ["catalina.sh", "run"]

#ENTRYPOINT ["/bin/sh"]
# Use sh - because windows has issues with +x on the script
CMD ["bash", "-c", "/home/forgerock/openam/boot.sh"]