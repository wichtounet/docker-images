FROM gentoo-hardened

MAINTAINER Baptiste Wicht

# Install and configure PostgreSQL 9.4.2
RUN emerge "=dev-db/postgresql-9.4.3"
RUN yes | emerge --config "=dev-db/postgresql-9.4.3"

# Allow remote connections
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql-9.4/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql-9.4/postgresql.conf

# Create volumes for data
VOLUME ["/var/lib/postgresql"]
VOLUME ["/run/postgresql"]

# Save some space
RUN rm -rf /usr/portage/distfiles/*

# Add the run-script
ADD pgsql-run /pgsql-run
RUN chmod 755 /pgsql-run

# Expose the PostgreSQL port
EXPOSE 5432

# Run postgres directly
CMD /pgsql-run
