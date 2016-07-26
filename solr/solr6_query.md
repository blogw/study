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