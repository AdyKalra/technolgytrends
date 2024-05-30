### Services Catalog
[Backstage](https://www.thoughtworks.com/radar/platforms/backstage) from Spotify has been widely adopted as the preferred platform to host developer experience portals mostly for application/services catalogs.

- Backstage, on its own, is just a shell that hosts plugins and provides an interface to manage the catalog of assets that make up a platform ecosystem.
- Any entity to be displayed or managed by Backstage is configured in the catalog-info file, which contains data such as status, lifecycle, dependencies and APIs among other details.
- By default, individual entity descriptors are written by hand and usually maintained and versioned by the team responsible for the component in question.
- Keeping the descriptors up to date can be tedious and create a barrier to developer adoption. Also, there is always the possibility that changes are overlooked or that some components are missed entirely.
- We've found it more efficient and less error-prone to automatically generate Backstage entity descriptors. Most organizations have existing sources of information that can jump-start the process of populating catalog entries.
- Good development practices, for example, putting appropriate tags on AWS resources or adding metadata to source files, can simplify entity discovery and descriptor generation. These automated processes can then be run on a regular basis — once a day, for example — to keep the catalog fresh and up to date.
