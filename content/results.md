## The TREE specification
{:#results}

We introduce the TREE hypermedia specification to fragment a collection of members in more interesting ways than only simple pagination.
It allows to qualify relations from the current `tree:Node`---a page or fragment that can be requested using HTTP GET---to multiple other pages, similar to search trees. 
The description allows for a user agent to understand that, when following the link, all members of the collection from that page on will respect a certain condition, such as the fact that the name contains a certain prefix, a value from a literal will be greater or less than a certain value, or is contained in a certain geospatial area.
The full specification can be found in the [TREE specification](https://w3id.org/tree/specification).
A concise overview of the specification is depicted in [](#treespec).

<figure id="treespec">
<div  style="width:100%; text-align:center">
<img src="https://docs.google.com/drawings/d/e/2PACX-1vR-iK_9kBzQXmaiUIo8U_jtBShONtD9PZlYlSyL9d3PfedqzJ_u1cXg9l_fKoK30dnLoBhFnagSOBkB/pub?w=1054&h=632" alt="The TREE specification" style="width: 100%">
</div>
<figcaption markdown="block">
TREE is a specification to qualify the relation between two pages. It is able to describe to a client whether following a certain page will not be interesting for its current query, and thus whether the client’s search space can be pruned.
</figcaption>
</figure>

### Collection design

The core collection design is largely inspired by and in line with Hydra.
An instance of a `tree:Collection` links using the `tree:member` to the entities it contains.

As a collection will grow too large for one page, a predicate needs to indicate the current page is a subset of the collection, and only one way through which the collection can be viewed.
When all members starting from this `tree:Node` can be found, the property `tree:view` can be used, meaning this node can be a starting point for _viewing_ all members of the collection.
Otherwise, if not all members can be found from that `tree:Node`, but if this node also contains a subset of the members in the collection, the property `void:subset` can be used.

### Discovery

A `tree:Collection` is a subclass of a `dcat:Dataset`.
The specialization being that it adheres to this collection design.
When a `tree:Collection` is an ever-growing append-only collection of immutable members, it must be typed using the subclass `ldes:EventStream`.
A `tree:Collection`, and its subclasses, should define what their members look like using a [SHACL shape](https://www.w3.org/TR/shacl/).
This SHACL shape may prove useful when selecting datasets from a DCAT catalog, also called _dataset discovery_.

However, when there are multiple views defined, a `tree:ViewDescription` can be defined, which is a subclass of a `dcat:DataService`.
The specialization being that it describes a Web API on top of a `tree:Collection`, publishing all members.
If the intention of the view is to publish the event source, the sublass `ldes:EventSource` can be used as a type.
The type only says something about the intention of the server administrator, and can still contain any kind of structure.
Through the `tree:ViewDescription`, a user agent can select the right view for the task it has at hand, also called _view discovery_.

The last point in discovery is _interface discovery_ to discover the next links to follow from within the view itself.
This is explored in the next subsection on traversing the hypermedia structure.

### TREE traversal

We always write TREE with all caps to indicate we take inspiration from traversing search trees, but we cannot guarantee, and do not limit the TREE hypermedia specification to designing search trees.
Even however we would limit it to search trees, counting on the fact that server would not provide you circular references would be incredibly naive.
Therefore, a TREE user agent must always keep a history of nodes it already traversed, and _prune_ these nodes from its yet-to-be-visited queue.
Visited nodes may be readded to the queue if the user agent implements a cache invalidation strategy.

The `tree:Node` describing the current page is linked with the property `tree:relation` to an entity that is an instance of a subclass of a `tree:Relation`.
For example, for string search, we have defined the type `tree:SubstringRelation`.
A `tree:value` property on top of that relation defines the value to be used in a comparison function defined by the relation, to compare the needs of the user agent with the intention of the relation.
The `tree:path` describes the property path (using the [Shapes Constraints Language (SHACL) Property Paths specification](https://www.w3.org/TR/shacl/#x2.3.1-shacl-property-paths)) to be resolved starting from a member, on which this `tree:value` applies.
Mind that a certain `tree:Node` can occur multiple times across relations, and that this must be interpretted as a logical AND.
A code example of a relation can be found in [](#TREE-code-sample).

Given the list of nodes linked from the pages a user agent already visited, minus these nodes it already visited, it can prune that list further based on the constraints given to the task at hand (e.g., find all members starting with labels starting with the letters `Ghent`).

<figure id="TREE-code-sample" class="listing" markdown="block">
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
    tree:path (sosa:simpleResult) .
</code></pre>
<figcaption markdown="block">
A Turtle example of an `ex:ThisPage` that links to a `ex:NextPage` through a GreaterThanRelation. A client can assume it must follow the page if its task needs members with a `sosa:simpleResult` greater than `5.1234`, to be compared using the double datatype.
</figcaption>
</figure>
