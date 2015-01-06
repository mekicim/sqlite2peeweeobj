sqlite2peeweeobj
================
generate db class for peewee https://github.com/coleifer/peewee 

    import sqlite3

    con = sqlite3.connect('db.sqlite')

    with con:

    	cur = con.cursor() 
    	cur.execute("SELECT name FROM sqlite_master WHERE type='table'")
    	rows = cur.fetchall()
    	for row in rows:
    		if row[0]!='sqlite_sequence':
    			print "class "+row[0]+"(BaseModel):" 
    			cur.execute("PRAGMA table_info('"+row[0]+"')")
    			columns = cur.fetchall()
    			for column in columns:
    				if column[2]=="INTEGER":
    					print "\t"+column[1]+" = IntegerField()"
    				elif column[2]=="TEXT":
    					print "\t"+column[1]+" = TextField()"
    				elif column[2]=="CHAR":
    					print "\t"+column[1]+" = CharField()"
    				elif column[2]=="Timestamp":
    					print "\t"+column[1]+" = DateTimeField(default=datetime.datetime.now)"
    			print "\n"





