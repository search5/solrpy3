# solrpy

[![Build Status](https://travis-ci.org/edsu/solrpy.svg)](http://travis-ci.org/edsu/solrpy)

solrpy is a Python client for [Solr], an enterprise search server
built on top of [Lucene].  solrpy allows you to add documents to a
Solr instance, and then to perform queries and gather search results
from Solr using Python.

## Overview

Here's the basic idea:

```python
import solr

# create a connection to a solr server
s = solr.SolrConnection('http://example.org:8083/solr')

# add a document to the index
doc = {
  "id": 1,
  "title": "Lucene in Action",
  "author": ["Erik Hatcher", "Otis Gospodnetić"]
}
s.add(doc, commit=True)

# do a search
response = s.query('title:lucene')
for hit in response.results:
    print hit['title']
```


## More powerful queries

Optional parameters for query, faceting, highlighting and more like this
can be passed in as Python parameters to the query method.  You just need
to convert the dot notation (e.g. facet.field) to underscore notation
(e.g. facet_field) so that they can be used as parameter names.

For example, let's say you wanted to get faceting information in your
search result::

```python
response = s.query('title:lucene', facet='true', facet_field='subject')
```

and if the parameter takes multiple values you just pass them in as a list::

```python
response = s.query('title:lucene', facet='true', facet_field=['subject', 'publisher'])
```

## Tests

To run the tests, you need to have a running solr instance. The easiest
way to do this is:

```
curl -sSL https://raw.githubusercontent.com/moliware/travis-solr/master/travis-solr.sh | SOLR_VERSION=4.10.3 SOLR_CONFS=tests bash
```

## Community

Feel free to join our [discussion list] if you have ideas or suggestions.

[Solr]:  http://lucene.apache.org/solr/
[Lucene]:  http://lucene.apache.org/java/docs/
[discussion list]:  http://groups.google.com/group/solrpy
