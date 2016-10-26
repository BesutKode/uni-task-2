# Elimination task 2

## Task

Build a GitHub repository about an island of Indonesia that is missing
from OpenStreetMap.

## Objective

This task assists participants gain an advanced understanding of
geospacial data, data formats, data quality, and an appreciation of
the status of Open Data in Indonesia.

This task provides participants with the opportunity to create an island
in OpenStreetMap, but this is not required.

## Background

[OpenStreetMap](https://en.wikipedia.org/wiki/OpenStreetMap) (OSM)
is a map of the world, created by people like you, and free to use under
the open license [odbl](http://opendatacommons.org/licenses/odbl/).

The data can be easily [queried](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL)
and visualised using [overpass turbo](http://overpass-turbo.eu/).

OSM objects can include metadata 'tag' that link the OSM object to other
systems, such as the `wikidata` and `wikipedia` tag that links the object
to those respective Wikimedia projects.

A OSM relation object is the most stable type of OSM object, and Wikidata
includes links to OSM relations.  The two other types of OSM objects are
ways and nodes, which are not stable and are not permitted in Wikidata.

The following query finds all 'relation' objects that are islands of Indonesia,
that have a Wikidata or Wikipedia identifier.

```
area[name="Indonesia"];
(
  relation
    [place=island]
    [name]
    [wikipedia]
    (area);
  relation
    [place=island]
    [name]
    [wikidata]
    (area);
 );
(>;);
out body;
```

The result is very large and map cause your browser to freeze.
The geojson result of that query is stored in the `uni-task-2` repository,
and may be loaded in any GIS tool on your desktop.

You can view the rendered map from that query in the small file
[`wikimedia_connected_island_relation.png`](wikimedia_connected_island_relation.png)
in the `uni-task-2` repository, showing that many islands of Indonesia
do not have an island object that is connected to Wikimedia projects.

The repository also has the query and geojson for ways that are islands, and
are connected to Wikimedia projects.

Another useful query is all coastline data of Indonesia, and related objects:

```
area[name="Indonesia"];
(
  way
    [natural=coastline]
    (area);
 );
(._;>;);
out body;
```

This is stored in `coastline.geojson`.
It is August data.

There is also relations and ways that are not connected to Wikimedia projects
that might be useful for this task.

## Steps

### Accept invite

You will receive an email from GitHub Classroom, inviting you to do
an assignment in the GitHub BesutKode organisation.

You need to accept that invitation.

Accepting that invitation will create a new private repository for you,
*however* it will be converted to a public repository on 20 November 2016.

Note there is [a bug](https://github.com/education/classroom/issues/729)
in GitHub Classroom that causes duplicate repositories to be created.
If you have multiple repositories created, do not use the repository with
suffix `-1` (etc).  They will be deleted by the Besut Kode admin team.

Everything you do will be public forever.

DO NOT link to an Issue or Pull Request of another repository.

There is a "slack" team for this task, only accessible by participants of
Besut Kode Universitas that have completed task 1:

https://besutkode.slack.com/messages/uni-task-2/

You will receive an invite from slack to join this team.

This channel is private.

Behave professionally and collegially.

You have been given administrative rights on your assignment repository.

DO NOT add collaborators to your respository.  This will result in immediate
disqualification.  If you want to share data or code with other participants,
use the `uni-task-2` repository.

## Activate Travis CI Pro

You should enable Travis CI Pro on your repository.

Then create a branch "citest" and confirm that it is running jobs correctly.

The BesutKode plan with Travis CI Pro only allows one concurrent build,
so please enable and disable it in your Travis CI Pro preferences
as needed to avoid running long jobs for little insignificant commits
to your repository.

Use it when you need it, to do a full build.

## Find a missing island

Use the data provided, and overpass turbo queries, to find an island of
Indonesia that:

- is not a relation object in OpenStreetMap
- is not connected to Wikimedia
- is more than 10 kms in length, or is 10 kms away from another island
- has more than 1,000 residents

If you find a relation that is only missing a connection to Wikimedia, you
are encouraged to edit the OpenStreetMap relation and add the missing
connection.  This helps you eliminate the object from further queries by
yourself and other participants.

An existing way object is ideal for this task, as it already contains the shape
data that is already licenced under the correct open data license.

### Register your project

Only one participant may work on an island.
This is to avoid duplicated and wasted effort by participants.

To prevent multiple participants doing the same island,
each participant will create a page on the BesutKode repository wiki
about the island they have selected before commencing work.

Once you have found an eligible island, first search the
[uni-task-2](https://github.com/BesutKode/uni-task-2) wiki
to check if someone else has already chosen the same island.

If nobody else has already selected the same island,
create a page on the wiki named with your GitHub username,
and include the following:

1. The name of your island
2. The province and regency(ies) of the island
3. Link to the Wikidata item about the island (create the item if it is missing) 
5. Link to any Wikipedia pages that are about the island
6. An estimated population size, with links as evidence
7. Any other information you believe is relevant.

Writing in bahasa Indonesia is acceptable.

Create a wiki page in `uni-task-2` about your island,
with evidence that it meets the criteria above.

## Populate your repository

Your repository should contain a well documented collection of *open* data
about your island, always describing where any data came from
(both attribution, and provenance), and the license of the data.

If a relevant dataset is hosted in a reliable publicly accessible
version controlled system, such as GitHub and OpenStreetMap, it is
not necessary to copy the data into your repository.

Create a program or script or query, in any programming language,
to extract relevant data from those open data datasets to
create a GeoJSON (or similar format) file that has:

- an accurate shape for the island, using public domain or ODBL data
- two additional sets of information about the island, using any open data

The file should be stored in your repository.

For example, on your island map, you might add:

- administrative borders if the island has multiple regencies or districts
- postal regions
- approximate regions of ethic or language groups
- protected areas
- lakes or mountains
- ship-wrecks

The sets of information included must be comprehensive,
and "data driven", based on documented and sensible critera.

It is acceptable to only show mountains above a certain reasonable size
that you select.  It is not acceptable to arbitarily select a few mountains.

If any part of your data processing is not automated, document the manual steps
used in excruciating detail, so that someone else could easily follow the same
procedure and obtain the same results.  Your results must be verifiable.

The automated steps of your process should be performed on Travis CI.

Do *NOT* create an island relation in OpenStreetMap without permission
from @jayvdb.  The process you used to create the geoshape will need to be
verified, otherwise your island may violate the legal framework of OSM,
and will need to be deleted.
See [Legal_FAQ](https://wiki.openstreetmap.org/wiki/Legal_FAQ).
This task does not require that you upload the island into OpenStreetMap.

## Create a presentation

Build an application that visualises your raw data.

The simplest method is a HTML page that uses
[OpenLayers](https://en.wikipedia.org/wiki/OpenLayers) to create custom maps.

However you are free to build a graphical application in any programming
language.

The application must be built on Travis CI Pro.

The application must be MIT licensed.

## Assessment

When you believe you have finished, run a fresh build in Travis CI of your
latest commit.  It *must* be green.

Create an issue in the Besut Kode `uni-task-2` repository assigned to @jayvdb.

The title of your issue should be your GitHub username, and the body
of your issue should be a link to your wiki page.

DO NOT link to an Issue or Pull Request of another repository.

John will check your lated Travis CI builds, which *must* be green.

The assessment will review that the process used to create the geoshape and
associated sets of information is predominately sourcing the data from
open data, or data presumed to be public domain and open.

The island shape will be compared with commercial map data to ensure that it is
similar, but is not the same.

The application will be viewed to ensure that the data curated in your
repository is presented to the user in the application.

## StackExchange

Geospacial Information Q&A is primarily covered by
[gis.stackexchange.com](http://gis.stackexchange.com/), which is a sister
website of StackOverflow.

### Related StackOverflow tags

- [openstreetmap](http://stackoverflow.com/questions/tagged/openstreetmap)
- [wikidata](http://stackoverflow.com/questions/tagged/wikidata)
- [gis](http://stackoverflow.com/questions/tagged/gis)
- [travis-ci](http://stackoverflow.com/questions/tagged/travis-ci)
- [bash](http://stackoverflow.com/questions/tagged/bash)
