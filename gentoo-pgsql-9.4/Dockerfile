FROM gentoo-hardened

MAINTAINER Baptiste Wicht

# Install and configre Postgresql
RUN mkdir -p /usr/portage/{distfiles,metadata,packages}; \
    chown -R portage:portage /usr/portage; \
    echo "masters = gentoo" > /usr/portage/metadata/layout.conf ; \
    emerge-webrsync -q ; \
    env-update ; \
    emerge "=dev-db/postgresql-9.4.3" ; \
    yes | emerge --config "=dev-db/postgresql-9.4.3"; \
    rm -rf /usr/portage/ ;

# Allow remote connections
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql-9.4/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql-9.4/postgresql.conf

# Create volumes for data
VOLUME ["/var/lib/postgresql"]
VOLUME ["/run/postgresql"]

# Add the run-script
ADD pgsql-run /pgsql-run
RUN chmod 755 /pgsql-run

# Expose the PostgreSQL port
EXPOSE 5432

# Run postgres directly
CMD ["/pgsql-run"]
