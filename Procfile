web: unicornherder --gunicorn-bin ./venv37/bin/gunicorn -p /var/run/ckan/unicornherder.pid wsgi:application --bind=localhost:${CKAN_PORT} --preload --pythonpath=/var/ckan --timeout ${GUNICORN_TIMEOUT} --workers ${GUNICORN_WORKER_PROCESSES} --log-file /var/log/ckan/app29.out.log --error-logfile /var/log/ckan/app29.err.log
pycsw_web: unicornherder --gunicorn-bin ./venv37/bin/gunicorn -p /var/run/ckan/pycsw_unicornherder.pid -- pycsw.wsgi -e PYCSW_CONFIG="/var/ckan/pycsw.cfg" --bind localhost:${PYCSW_PORT} --timeout ${GUNICORN_TIMEOUT} --workers ${GUNICORN_WORKER_PROCESSES} --log-file /var/log/ckan/pycsw29.out.log --error-logfile /var/log/ckan/pycsw29.err.log

harvester_gather_consumer: ./venv37/bin/ckan -c ${CKAN_INI} harvester gather-consumer
harvester_fetch_consumer: ./venv37/bin/ckan -c ${CKAN_INI} harvester fetch-consumer
