# Draft Plan of Decentralizing LCSH

## Scope

- **Key Goal**: Pull out LCSH data, convert to IPLD, then load into IPFS. Write up, informally, method, snags, pluses, etc.
- **Secondary Goal**: Informs planning for data.gov metadata management post-data.gov captures in IPFS.
- **Secondary Goal**: Sketch edges of how cultural heritage repository systems can manage distributed authority datasets references, e.g. Fedora 4 calling to Cornell's preferred data version of a LCNAF resource.

## Questions

- LCSH == Library of Congress Subject Headings and Library of Congress Name Authority File (just clarify)
- Do we want to manage RWOs and Authorities, or just Authorities, or whatever we can harvest from id.loc.gov?
    - LC Name Authority File (MADS/RDF only) downloaded from http://id.loc.gov/download/ - Download link is http://id.loc.gov/static/data/authoritiesnames.nt.madsrdf.gz - gives us only Authorities, no RWOs per 'http://id.loc.gov/rwo/agents/no2011069838' and not even assertions with 'http://www.loc.gov/mads/rdf/v1#identifiesRWO'.
    - That download is out-of-date as well as being lossy data.
- Do we want their LOD or the originating MARC to then convert to more granular LOD? (lossiness quotes/analysis here?)
- How to check for updates to LCSH and where those go into our IPFS/IPLD data.
- What does this require of institutions wanting to use canonical LC URIs for resources but retrieve a IPFS fork of the data? I.E. MARC $0 with a LC URI but an indexing system that wants to query instead our IPFS copy?

## Work Areas

- GitHub Repository for Authenticated Metadata: https://github.com/ipld/authenticated-metadata/
-

## Steps

1. Document work plan in GH repo, get confirmation among partners of next steps.
    2. Blog plan in TBD platform for sharing updates and notifying community of the work being planned, attempted.
2. Downloaded id.loc.gov datasets.
    a. To TBD working space.
    b. Only LCNAF and LCSH? Seems easiest place to start.
    c. Only MADSRDF? SKOS? Originating MARC (no data dump for that)?
        i. MADSRDF seems best middle-ground of this issue.
        ii. Need to document how to handle pulling non-LC to then convert to better representation of LC would be good.
    c. Add RWOs?
3. Perform and share analysis of what metadata/data is there for sake of clarifying next steps and questions.
4. Add to IPFS:
    5. To local IPFS repository then pushed to TBD shared IPFS repository?
    6. Pre-processing: split into records? normalize at all? dictated by tracking changes expected from id.loc.gov?
7. Write to IPLD:
    8. Convertor for MADSRDF to IPLD?
    9. What about meta-metadata? Two repos? two directories?
    10. Can IPLD handle multiple pointers? i.e. {"/": /ipfs/hash/test-ipld/n1234567.ipld} points meta-metadata to the metadata itself post-conversion to ipld, can we also have {"/source": /ipfs/hash/lc-ipld/n1234567.madsrdf.nt} for the originating file we converted?
    11. If we have both, how do we propogate changes while keeping paths unique?
    13. Do we have our recommended data model that extends IPLD?
14. Forking and handling data changes, requests to update, pulling in new updates:
    15. What does it look like then to fork an authority dataset - create a new meta-directory, add your meta-metadata, and get sources you want, then run your own convertors?
    16. Go grab updated metadata from id.loc.gov (able to do at URI-specific level at this point) and see/document how to handle propogation of changes, handling conflicts.
    17. Go grab original MARC for each URI, convert to more granular MADSRDF, and see/document how to merge with test-ipld and test-MADSRDF.
    18. Figure out and document how one would restrict merging, updating of specific directories or repositories, and where that fits in our meta-metadata model.
18. Interacting with the authority data:
    19. Explore how Fedora would make requests to a LC URI but need to know to instead check the specified IPLD/IPFS directory at the appropriate key then pull that data back instead (if found).
    20. Explore the same question as above but with a BIBFRAME convertor reconciliation module.
21. See how lessons learned from this apply to data.gov datasets, and sketch out a plan for distributed metadata that describes the datasets captured in various ipfs repositories.