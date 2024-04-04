### Guidance

<!-- {% raw %} to make the USCDI table

need 

source CSV file = `input/data/uscdi-table.csv`
markdown page file = `input/pagecontent/uscdi.md`
liquid template files = `input/includes/uscdi-uscore-map.html`,`input/includes/sd_link.html`
icons (png files) = `input/images/<"kebab case" USCDI class names>.png`

1. create the source CSV file with all the same column names
    - FHIRPath column is not used for rendering so can replace with template name or whatever
    - this file lives in the `input/data` folder
    - It is copied to the `input/images` folder as both a csv and convert to excel file using a bash/python script.
2. The pagecontent/uscdi.md page is where the table is rendered
3. the liquid template tag "{% include uscdi-uscore-map.html %}" references `includes/uscdi-uscore-map.html` which does the rendering
   - this file depends on another liquid template {% include sd_link.html title = title  %} which refererence `includes/sd_link.html` to get the profile page link.
   1. icons (png images) are in the `input/images` are named using the "kebab case" USCDI class names.

The US Core Profiles were originally designed to meet the 2015 Edition certification criterion for Patient Selection 170.315(g)(7) and Application Access – Data Category Request 170.315(g)(8). They were created for each item in the [2015 Edition Common Clinical Data Set (CCDS)]. The Location, Organization, and Practitioner Profiles are not called out specifically in the certification criteria but are included because other profiles directly reference them. The US Core Profiles are informed by the prior [Data Access Framework] and the [Argonaut Data Query] Implementation Guides. However, the profiles here are stand-alone and include requirements from the [U.S. Core Data for Interoperability (USCDI) v4].

The table below lists the US Core Profile and FHIR Resources used for the corresponding USCDI Data elements. This information is also available as a [csv](uscdi-table.csv) or [excel](uscdi-table.xlsx) file:

{% include uscdi-uscore-map.html %}

{% endraw %} -->



### Referencing US Core Profiles
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Contained Resources
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Suppressed Data
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### SNOMED CT United States Edition
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

#### SNOMED CT Edition and Version Options
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

###  Using UCUM codes in the [Quantity] datatype
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Representing Deleted Information

A FHIR Server **SHOULD** not delete records. A FHIR server **SHOULD** update the appropriate resource status to `entered-in-error` or `inactive` (refer to the next section on *Representing Entered in Error Information*). If a system supports the deletion of records, they **SHOULD** refer to the [Deletion Safety Checks] in the FHIR specification.

### Representing Entered in Error Information

Clinical information that has been entered in error in the patient's record needs to be represented by the FHIR Server in a way so that Clients can expose the corrected information to their end users.

**Server Recommendations:**
- A FHIR Server **SHOULD** not delete resources.
- A FHIR server **SHOULD** update the appropriate resource status to `entered-in-error` or `inactive`.
- A FHIR Server **SHOULD** allow these resources to be searchable by client applications.
- If the FHIR server has updated the resource status to `entered-in-error`:
    -  For *patient facing* applications, A FHIR Server **SHOULD** remove the contents of resource leaving only an id and status.   Note this typically will not be conformant with the US Core or FHIR StructureDefinitions.
    - For *provider-facing* applications,  the content may be supplied with content and additional detail (such as the reason for the status change) that the patient viewing system would typically not have access to.


### Narrative
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Language Support
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Timezone and Time Offsets (*STRAWMAN PROPOSAL*)
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Read (Fetch) Syntax
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Search Syntax
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Searching Multiple Patients
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh

### Searching Multiple Patients
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh

### Searching using lastUpdated

<div class="bg-success" markdown="1">

Servers that can accurately populate [`Meta.lastUpdated`](#) **SHOULD** support the [`_lastUpdated`](#) search parameter as defined in the core FHIR specifications. If `Meta.lastUpdated` is populated:
<!-- - Any change in the resource implies a change in `Meta.lastUpdated`; conversely, an unchanged `Meta.lastUpdated` implies no change in the resource. -->
- Note to clients that the most recent time does not necessarily reflect changes they can access. A record may change, but the client's view of the resource may not (for example, if the client is not authorized to see the changed data).
<!-- - Servers cannot populate `Meta.lastUpdated` if they cannot update it per the rules in the FHIR core specification. -->
- Supporting `Meta.lastUpdated` in a resource does not imply support for searches using the `_lastUpdated` search parameter.
- Support for searches using the `_lastUpdated` search parameter does not require servers to support `Meta.lastUpdated`; servers can use an alternative method to reliably track changes to an instance.
- Note to servers that updating the timestamp too frequently is better than missing updates.

<div class="stu-note" markdown="1">
Many servers are unable to populate the `Meta.lastUpdated` element accurately. However,
they **SHOULD** expose a method for clients to know if there are new or modified resources since their last polling time and advertise that mechanism in their CapabilityStatement.  Work is in progress to:
- Enable [FHIR Topic-Based Subscription](#) for notifications on relevant events as an alternative to search polling.
</div><!-- stu-note -->

</div><!-- new-content -->

### Compartment Based Search
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Across Platform Searches
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc imperdiet nunc at massa porta rutrum. Duis ac nulla a velit hendrerit vehicula at nec urna. Sed gravida pellentesque molestie. Praesent commodo, sem et tincidunt vulputate, nisl nibh 

### Limiting The Number Of Search Results


{% include link-list.md %}