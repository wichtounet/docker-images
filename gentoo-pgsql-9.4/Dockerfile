FROM gentoo-hardened

MAINTAINER Baptiste Wicht

# Install and configure PostgreSQL 9.4.2
RUN emerge "=dev-db/postgresql-9.4.3"
RUN yes | emerge --config "=dev-db/postgresql-9.4.3"

# Allow remote connections
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql-9.4/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql-9.4/postgresql.conf

# Fix permissions
RUN chown -R postgres:postgres /var/lib/postgresql/
RUN chmod -R 700 /var/lib/postgresql/

# Expose the PostgreSQL port
EXPOSE 5432

# Install sudo (for the run script)
RUN emerge app-admin/sudo

# Save some space
RUN rm -rf /usr/portage/distfiles/*

# Add the run-script
ADD pgsql-run /pgsql-run
RUN chmod 755 /pgsql-run

# Run postgres directly
CMD /pgsql-run
