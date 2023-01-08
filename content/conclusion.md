## Conclusion
{:#conclusion}

Materializable → because it doesn’t need to be materialized, but it can.
It only requires computational power to be updated. The rest _can_ just be file-based.
This turns the four challenges into four advantages:

 1. __Querying your end-user’s world__<br/>
When a user agent performs the query processing, it can execute the queries using the datasets that matter most to them.
 2. __Archivable__<br/>
Materializable means everything can be generated in files without the need for dynamic server functionality.
 3. __Evolvable__<br/>
A client is always going to start from a root node.
 4. __Query privacy__:
The only thing a server sees is that a client is interested in a certain part of its dataset.

The current version of the TREE vocabulary has been submitted to [LOV](cite:cites lov).
In order to further evolve the specification, we are now starting a TREE/LDES community group at W3C.

We will also need workflows. What to use exactly is... but the result and the provenance can be described using DCAT, SHACL, PROV-O , P-Plan, SDS (cite!), etc. Data privacy DPV, access control, etc.
