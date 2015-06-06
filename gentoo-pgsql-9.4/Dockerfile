FROM gentoo-hardened

MAINTAINER Baptiste Wicht

# Install PostgreSQL 9.4.2
RUN emerge "=dev-db/postgresql-9.4.3"

# Run as postgres
USER postgres

# Allow remote connections
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.4/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/postgresql.conf

ADD pgsql-run /pgsql-run
RUN chmod 755 /pgsql-run

# Expose the PostgreSQL port
EXPOSE 5432

# Run postgres directly
CMD /pgsql-run