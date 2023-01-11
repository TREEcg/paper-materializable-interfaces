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
A user agent is going to start from an entry pointt node, and will be able to 
 4. __More query privacy__<br/>
The only thing a server sees is that a client is interested in a certain part of its dataset.

## Future work
{:#future-work}

The current version of the TREE vocabulary has been submitted to [LOV](cite:cites lov).
In order to further evolve the specification, we are now starting a TREE/LDES community group at W3C.

The last information on the TREE hypermedia project can be found at https://tree.linkeddatafragments.org.
In future work, we are also going to tackle graph-based and time series fragmentations with the TREE/LDES method.
Furthermore, the [Comunica Querying engine](cite:cites taelman_iswc_resources_comunica_2018) is being extended with a TREE hypermedia querying actor that does query planning across multiple hypermedia interfaces.
