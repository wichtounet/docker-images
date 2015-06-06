FROM gentoo-hardened

MAINTAINER Baptiste Wicht

# Install and configure PostgreSQL 9.4.2
RUN emerge "=dev-db/postgresql-9.4.3"
RUN echo "y" | emerge --config "=dev-db/postgresql-9.4.3"

# Add the run-script
ADD pgsql-run /pgsql-run
RUN chmod 755 /pgsql-run

# Allow remote connections
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql-9.4/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql-9.4/postgresql.conf

# Expose the PostgreSQL port
EXPOSE 5432

# Install sudo (for the run script)
RUN emerge app-admin/sudo

# Save some space
RUN rm -rf /usr/portage/distfiles/*

# Run postgres directly
CMD /pgsql-run
