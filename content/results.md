## The TREE specification
{:#results}

We introduce the TREE hypermedia specification depicted in [](#tree-ontology).
Using the vocabulary, relations can be described, linking other fragments to the current fragment.
The description allows for a client to understand that, when following the link, all members of the collection from that page on will respect a certain condition, such as the fact that the name starts with a certain prefix.
The TREE specification uses the triple-based RDF as its knowledge representation model, enabling different serialization to be used, as well as compatibility with existing Linked Data domain models.
The full specification can be found in the [TREE specification](https://w3id.org/tree/specification).

<figure id="tree-ontology">
<div  style="width:100%; text-align:center">
<img src="https://docs.google.com/drawings/d/e/2PACX-1vR-iK_9kBzQXmaiUIo8U_jtBShONtD9PZlYlSyL9d3PfedqzJ_u1cXg9l_fKoK30dnLoBhFnagSOBkB/pub?w=1054&h=632" alt="The TREE specification" style="width: 100%">
</div>
<figcaption markdown="block">
TREE is a specification to qualify the relation between two pages. It is able to describe to a client whether following a certain page will not be interesting for its current query, and thus whether the client’s search space can be pruned.
</figcaption>
</figure>

{:TODO HERE}
DDD
{:TODO}
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
A code example of a relation can be found in [](#TREE-code-sample).

<figure id="TREE-code-sample" class="listing">
<pre><code>
@prefix tree: <https://w3id.org/tree#>.
@prefix ex: <http://example.org/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@prefix sosa: <http://www.w3.org/ns/sosa/>.

ex:C a tree:Collection ;
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
