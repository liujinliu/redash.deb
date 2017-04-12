# the order should be
# 1.create_user
# 2.venv
# 3.package_install_pre
# 4.package_install
# 5.create_database

COOKIE_SECRET=$(shell pwgen -1s 32)

create_user:
	adduser --system --no-create-home --disabled-login --gecos "" redash

create_database:
	sudo -u postgres createuser redash --no-superuser --no-createdb --no-createrole
	sudo -u postgres createdb redash --owner=redash
	cd /opt/redash/current && sudo -u redash bin/run ./manage.py database create_tables && cd -

venv:
	virtualenv --no-site-packages /opt/venv/redash

package_install_pre:
	chown redash /opt/redash
	cp /opt/redash/conf/.env /opt/redash/
	echo "export REDASH_COOKIE_SECRET=${COOKIE_SECRET}" >> /opt/redash/.env
	ln -nfs /opt/redash/.env /opt/redash/current/.env

package_install:
	. /opt/venv/redash/bin/activate && pip install setproctitle
	. /opt/venv/redash/bin/activate && pip install -r /opt/redash/current/requirements.txt
	. /opt/venv/redash/bin/activate && pip install -r /opt/redash/current/requirements_all_ds.txt

