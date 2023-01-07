## The TREE specification
{:#results}

We introduce the TREE hypermedia specification depicted in [](#tree-ontology).
Using the vocabulary, relations can be described, linking other fragments to the current fragment.
The description allows for a client to understand that, when following the link, all members of the collection from that page on will respect a certain condition, such as the fact that the name starts with a certain prefix.
The TREE specification uses the triple-based RDF as its knowledge representation model, enabling different serialization to be used, as well as compatibility with existing Linked Data domain models.
The full specification can be found in the [TREE specification](https://w3id.org/tree/specification).

<figure id="tree-ontology">
<div  style="width:100%; text-align:center">
<img src="https://docs.google.com/drawings/d/e/2PACX-1vTTCjBkBum1J4xgbg0oZJaD_H05dpZxhL6jrp1yzqoIsYw5EOa-7D24No_rfEyTipq1rLb-_tPTEYV0/pub?w=1093&h=546" alt="The TREE specification" style="width: 100%">
</div>
<figcaption markdown="block">
TREE is a specification to qualify the relation between two pages. It is able to describe to a client whether following a certain page will not be interesting for its current query, and thus whether the client’s search space can be pruned.
</figcaption>
</figure>

<figure id="TREE-code-sample" class="listing">
<pre><code>ex:C a tree:Collection ;
    tree:view ex:ThisPage .

ex:ThisPage a tree:Node ;
    tree:relation ex:Relation1 .

ex:Relation1 a tree:GreaterThanRelation ;
    tree:node ex:NextPage ;
    tree:value "5.1234"^^xsd:double ;
    tree:path (sosa:simpleResult) .</code></pre>
<figcaption markdown="block">
A Turtle example of an `ex:ThisPage` that links to a `ex:NextPage` through a GreaterThanRelation. A client can assume it must follow the page if its task needs members with a `sosa:simpleResult` greater than `5.1234`, to be compared using the double datatype.
</figcaption>
</figure>

### Collection design

We need a collection design to be described in RDF.

!!! Can we build the rationale for not working triple based? Member based is the way.

We should not do triple-based.

A collection has a view, etc.


### Traversing

A `tree:Node` is linked to a `tree:Collection`,<!-- though three different predicates: `dcterms:isPartOf`, `void:subset` or `tree:view`.-->
which can be found from discovery results from W3C specifications such as DCAT, Activity Streams 2.0, Web of Things, Hydra, SPARQL resultsets and Triple Pattern Fragments.
<!--The first two are equivalent yet inverse predicates, stating this page is part of the full collection.-->
Only the specific predicate `tree:view` guarantees that from this node on, all members of the collection can be found.
<!--The `tree:Collection` can thus be found using this SPARQL property path expression: `?collection void:subset|tree:view|^dcterms:isPartOf <page_url> .`-->
With the predicate `tree:member`, elements of this collection can be found in the current page.
The `tree:Node` describing the current page is linked with the predicate `tree:relation` to other pages.
The object is a subclass of `tree:Relation`.
For string search, we have defined the type `tree:PrefixRelation`.
A `tree:value` predicate links a specific string to this relation: the string is a prefix of all further members in the collection.
The `tree:path` describes the property path (using the [Shapes Constraints Language (SHACL) Property Paths specification](https://www.w3.org/TR/shacl/#x2.3.1-shacl-property-paths)) on which this `tree:value` applies.

### Splitting live data

For string comparisons with tree:PrefixRelation or tree:SubstringRelation, by default, unicode order is followed, yet specific flags can change the order for options such as case-sensitivity, as [documented in the TREE specification](https://github.com/pietercolpaert/TreeOntology/blob/master/specs/2-traversing.md#comparing-strings).
For geospatial comparisons with tree:GeospatiallyContains, a geosparql:wktLiteral is expected.

Write about:
 * tree:embed
 * tree:import
 * tree:qualifiedValue

Write about:
 * Search forms
