FROM apache/superset:6.0.0

USER root

RUN . /app/.venv/bin/activate && uv pip install --no-cache-dir duckdb==1.4.3 duckdb-engine==0.17.0 pyhive sqlalchemy-bigquery trino psycopg2-binary

COPY --chown=superset superset_config.py /app/
ENV SUPERSET_CONFIG_PATH=/app/superset_config.py

USER superset
