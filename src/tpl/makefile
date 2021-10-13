DBPATH=./db
DBPORT=5432
DBHOST=127.0.0.1
DBUSER=postgres
DBUSER=$(shell whoami)
DBNAM=test
PG_BINDIR=/usr/lib/postgresql/12/bin/
INITDB=$(PG_BINDIR)initdb
PG_CTL=$(PG_BINDIR)pg_ctl
PSQL=/usr/bin/psql
RM=/usr/bin/rm
#-U sa 
dbmk:
	$(INITDB) \
		$(DBPATH)
dbrm:
	$(RM) \
		-r $(DBPATH)
dbstart:
#	sudo -u postgres 
	$(PG_CTL) \
		-U $(DBUSER) \
		-D $(DBPATH) \
		-o "-p $(DBPORT)" \
		start
dbstop:
	$(PG_CTL) \
		-U $(DBUSER) \
		-D $(DBPATH) \
		-o "-p $(DBPORT)" \
		stop 
dbclient:
	$(PSQL) \
		-U $(DBUSER) \
		-h $(DBHOST) \
		-p $(DBPORT) \
		$(DBNAM)
dbvacuum:
	$(PSQL) \
		-U $(DBUSER) \
		-P pager=off\
		-h $(DBHOST) \
		-p $(DBPORT) \
		-d $(DBNAM)\
		-c "vacuum full;"
dbsize:
	$(PSQL) \
		-U $(DBUSER) \
		-P pager=off\
		-h $(DBHOST)\
		-p $(DBPORT)\
		-d $(DBNAM)\
		-c "select pg_database_size('$(DBNAM)'),pg_size_pretty( pg_database_size('$(DBNAM)'));"
dbls:
	$(PSQL) \
		-U $(DBUSER) \
		-P pager=off\
		-h $(DBHOST) \
		-p $(DBPORT) \
		-d postgres \
		-c "SELECT * FROM pg_catalog.pg_tables;"

dbdrop:
	$(PSQL) \
		-U $(DBUSER) \
		-P pager=off\
		-h $(DBHOST) \
		-p $(DBPORT) \
		-d postgres \
		-c "drop database $(DBNAM);"
dbinit:
#	sudo -u postgres 
#	$(PG_CTL) \
#		-U $(DBUSER) \
#		-D $(DBPATH) \
#		-o "-p $(DBPORT)" \
#		start
	$(PSQL) \
		-U $(DBUSER) \
		-P pager=off\
		-h $(DBHOST) \
		-p $(DBPORT) \
		-d postgres\
		-c "create database $(DBNAM);"
clean:
	$(RM) -r ./db ./bin
