## Abstract
<!-- Context      -->
Ever since the Web was introduced to access representations of resources via URLs, Web developers have been coming up with ways to make data more queryable via more complex URL patterns.
<!-- Need         -->
URL patterns with features such as the SPARQL query language, GraphQL, OGC Web Feature Services, or free text queries, also come with drawbacks:
i) you only query the data integrated on the machine you query,
ii) coding against a fixed protocol lowers potential evolvability,
iii) relying on dynamic server functionality raises challenges in long-term preservation, and
iv) sending the full query to a third party server lowers query privacy.
<!-- Task         -->
Linked Data Fragments puts forward the idea that there is a false dichotomy between solving the full query on the server of the data publisher and solving it fully on the infrastructure of the consumers:
when publishing data in fragments of triples in a dataset with a certain locality into an interlinked resource-structure, data consumers can speed up their own query processing by leveraging the locality of reference principle.
Linked Data Event Streams extends upon these ideas and proposes a priority shield for what fragmentations should be built first: i) a fragmentation that makes replication and synchronization efficient for other actors to build their own views, ii) fragmentations of such an event stream according, and iii) querying protocols.
<!-- Object       -->
In this paper, we build evolvable and preservable Web APIs using “materializable interfaces”.
<!-- Findings     -->
For use cases such as route planning, full-text search, geospatial look-ups or replication and synchronization, we show how to build a fragmentation using the TREE hypermedia specifications that can qualify the relation from one fragment to another.
<!-- Conclusion   -->
This way, the TREE hypermedia specification enables to overcome the four drawbacks of URL-based query protocols.
<!-- Perspectives -->
The specification will be further developed as part of a W3C community group for which we are now seeking support.

<!--
Future work
 → W3C community group around this: please support
 → Comunica support, etc.
-->

<!--Important note: by design we chose not to annotate triples. We believe we should always publish members in a collection described by triples.

I’m more and more starting to be convinced that we should never publish just “triples”, but that we should publish members of a collection described using triples. I’ve always struggled with how to position Triple Pattern Fragments and the likes properly in a data architecture, and how to describe what happens to your data when you fragment your data according to TPF. With TPF you think from the perspective of a query agent → I want to resolve this query pattern, so the server should give me these controls. You’re not
-->
