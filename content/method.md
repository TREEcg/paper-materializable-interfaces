## Building materializable interfaces
{:#method}

The TREE specification allows publishers to construct their own __materializable hypermedia interfaces__.
We define _a materializable interface_ as an interface that has a finite set of URLs that provide an answer.
That way, the interface can be published using a simple file host, but is also very efficient to be hosted through a content delivery network, even if the server itself is built in a dynamic way in which each GET request on a URL potentially triggers a script to be executed.

The strategies in which a dataset can be fragmented is infinite, similar to the amount of indexes one can make on top of a relational database.
One method of thinking about a fragmentation strategy, is __to only fragment a dataset from the moment a dataset becomes too large for one page.__
The way in which a second page will be added can then be decided based on the needs in the ecosystem.
As illustrated in [](#multiple-views-2), the first priority should be to build the relation to the second page based on how the dataset is growing.
That way, that fragmentation can be efficiently used for populating other Web APIs on top of that dataset.
However, when the event source is available, we can optionally support more functionality on top of the dataset

<figure id="multiple-views-2">
<img src="https://docs.google.com/drawings/d/e/2PACX-1vRALczK4l21HiH9OJxVPiosoCZqFGlEJ5JFV442OLTzNgEefWwgP1m10AQ17UikF1nd7JmNf4p7z9_Z/pub?w=884&h=296" />
<figcaption>
A space of materializable interfaces on top of Linked Data interfaces can be queried from the user agents.
</figcaption>
</figure>

The use cases we worked with included querying for geospatial relations, time schedules of public transit data, OpenStreetMap’s road network and taxonomies with text literals such as an address database, geonames, OpenStreetMap names or Wikidata entities.
These cases have been published in their respective papers, for which we provide a concise overview below (as of January 2023).
These use cases describe their search space `tree:Relation` objects.

 1. __Replicating and synchronizing dataset copies across organizations__<br/>
A one dimensional pagination of an ever-growing collection of immutable events has interesting caching properties.
Only one page remains to be polled, while all other pages are historic and can be flagged with the `cache-control: immutable` response header.
In [](cite:cites lonneville2021publishing) this is applied on Marine Regions: a gazetteer of standard marine georeference place names and areas. While different organizations build different views on it, all views only need to poll the last page to keep their views in-sync.
In [](cite:cites ldes) it is applied on top of both base registries of the Flemish government, as well as a sensor observation stream, proving the method is both useful for
In [](cite:cites van2022publishing) it is applied to keep the data from art collections from the city of Ghent in-sync with their digital asset management system and the city’s SPARQL endpoint, through which the history and the current state of the art collections can be queried.
In a similar way, for more fine-grained access to specific windows in time, a B+-tree like fragmentation can also be designed.
 2. __Time-based relations for route planning over public transit networks__<br/>
Public transit can be modeled as a temporal directed acyclic graph departures and arrivals. With [Linked Connections](cite:cites rojas2022publishing), we proposed to fragment this long list of connections from one stop to another in time intervals. A public transit route planner can then perform the route planning algorithm on the infrastructure of the user agent, by selecting the right time window and performing the route planning in a streaming manner, downloading more data when needed.
 3. __Geospatial relations for route planning over road and transit networks__<br/>
The [route planning use case](cite:cites delva2019client) illustrates the need for querying with a more open world while retaining query privacy.
By geospatially fragmenting a road network (such as OpenStreetMap), we can select data with a geospatial locality, and/or public transit with a time and geospatial locality.
The public transit data also needs a road network to potentially calculate walks to transfer from one public transit stop to another, and maybe that transfer needs to happen according to the potential constraints of the end-user, whether they are pushing a stroller, in a wheelchair, trained athletes, or visually impaired. However, the profile of user does not need to be leaked to a server in order for the route planning result to be calculated.
 4. __Substring-based relations for autocompletion__<br/>
Mutatis mutandis for [substring autocompletion](cite:cites dedecker2021file): the locality is now not based on geospatial or time-based literals, but on the basis of substring matches with a string literal. Similar benefits can be found.

All these interfaces can be kept in-sync thanks to the event source, but also need to be able to describe how they are derived from which sources.
The result of a workflow over [semantically describe streams can already be described](cite:cites vercruysse2022describing, guasch2022semantic) by combining LDES, DCAT, SHACL, PROV-O and P-Plan.
