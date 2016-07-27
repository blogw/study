#Solr Query#
---

###Indexing and Retrieving a Document###
	# add a document (also known as “indexing” a document)
	root@2006b56fecbd:~# curl http://localhost:8983/solr/liferay/update -d '
	[
	 {"id" : "book1",
	  "title_t" : "The Way of Kings",
	  "author_s" : "Brandon Sanderson"
	 }
	]'
	{"responseHeader":{"status":0,"QTime":56}}

	# ask for it back
	root@2006b56fecbd:~# curl http://localhost:8983/solr/liferay/get?id=book1
	{
	  "doc":
	  {
	    "id":"book1",
	    "title_t":["The Way of Kings"],
	    "author_s":"Brandon Sanderson",
	    "_version_":1540904994236006400}}

	# update a doc
	root@2006b56fecbd:~# curl http://localhost:8983/solr/liferay/update -d '
	[
	 {"id"         : "book1",
	  "cat_s"      : { "add" : "fantasy" },
	  "pubyear_i"  : { "add" : 2010 },
	  "ISBN_s"     : { "add" : "978-0-7653-2635-5" }
	 }
	]'
	{"responseHeader":{"status":0,"QTime":7}}

	# get back again
	root@2006b56fecbd:~# curl http://localhost:8983/solr/liferay/get?id=book1
	{
	  "doc":
	  {
	    "id":"book1",
	    "title_t":["The Way of Kings"],
	    "author_s":"Brandon Sanderson",
	    "cat_s":"fantasy",
	    "pubyear_i":2010,
	    "ISBN_s":"978-0-7653-2635-5",
	    "_version_":1540906122622271488}}

###Solr Search Requests###
	# update with csv
	root@2006b56fecbd:~# curl http://localhost:8983/solr/liferay/update?commitWithin=5000 -H 'Content-type:text/csv' -d '
	id,cat_s,pubyear_i,title_t,author_s,series_s,sequence_i,publisher_s
	book1,fantasy,2010,The Way of Kings,Brandon Sanderson,The Stormlight Archive,1,Tor
	book2,fantasy,1996,A Game of Thrones,George R.R. Martin,A Song of Ice and Fire,1,Bantam
	book3,fantasy,1999,A Clash of Kings,George R.R. Martin,A Song of Ice and Fire,2,Bantam
	book4,sci-fi,1951,Foundation,Isaac Asimov,Foundation Series,1,Bantam
	book5,sci-fi,1952,Foundation and Empire,Isaac Asimov,Foundation Series,2,Bantam
	book6,sci-fi,1992,Snow Crash,Neal Stephenson,Snow Crash,,Bantam
	book7,sci-fi,1984,Neuromancer,William Gibson,Sprawl trilogy,1,Ace
	book8,fantasy,1985,The Black Company,Glen Cook,The Black Company,1,Tor
	book9,fantasy,1965,The Black Cauldron,Lloyd Alexander,The Chronicles of Prydain,2,Square Fish
	book10,fantasy,2001,American Gods,Neil Gaiman,,,Harper'
	<?xml version="1.0" encoding="UTF-8"?>
	<response>
	<lst name="responseHeader"><int name="status">0</int><int name="QTime">46</int></lst>
	</response>

We added the commitWithin=5000 parameter to indicate that we would like our updates to be visible within 5000 milliseconds (5 seconds). The Lucene library that Solr uses for full-text search works off of point-in-time snapshots that must be periodically refreshed in order for queries to see new changes.
	
	# search by title
	root@2006b56fecbd:~# curl "http://localhost:8983/solr/liferay/query?q=title_t:black&fl=id,author_s,title_t"
	{
	  "responseHeader":{
	    "status":0,
	    "QTime":0,
	    "params":{
	      "q":"title_t:black",
	      "fl":"id,author_s,title_t"}},
	  "response":{"numFound":2,"start":0,"docs":[
	      {
	        "id":"book8",
	        "title_t":["The Black Company"],
	        "author_s":"Glen Cook"},
	      {
	        "id":"book9",
	        "title_t":["The Black Cauldron"],
	        "author_s":"Lloyd Alexander"}]
	  }}


###Dynamic Fields###
The “id” field is already pre-defined in every schema. Lucene and Solr need to know the types of fields so that they can be indexed in the correct way. There are a number of options for defining new fields:

- Edit the schema.xml file to define the fields.
- Use the Schema API to add the new fields.
- Use dynamicFields, a form of convention-over-configuration that maps field names to field types based on patterns in the field name. For example, every field ending in “_i” is taken to be an integer.
- Use “schemaless” mode, where field types are auto-detected (guessed) based on the first value seen for that field


###reference###
[solr-tutorial](http://yonik.com/solr-tutorial/)

###author###
[blogw](mailto:blogw@163.com) 2016/07/26