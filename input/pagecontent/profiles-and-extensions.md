### Profiles

The following profiles and have been defined for this implementation guide.

<!-- ================================================ -->
<!--  use this line to include an autogenerated list of all profiles and highlight new ones using the input/data/new_stuff.yml list.  Remove it if you would like to hand generate it -->

{% include sd-list-generator.md %}
<!-- ================================================ -->

<br />

### Extensions

 <!-- extension name paremeter ( not title) as comma separated string parameters --->
 <!-- passed in from the page used to define the extension for each section -->
 <!-- In future, made need to convert to data file as csv if gets bigger -->
{% assign ig_only = "USCDIRequirement" %}
{% assign realm_only = "USCoreDirectEmailExtension,USCoreJurisdictionExtension" %}

The following [Extensions]({{site.data.fhir.path}}extensibility.html) have been defined as part of the US Core implementation Guide. A [registry of standard extensions]({{site.data.fhir.path}}extensibility-registry.html) can be found in the FHIR specification and additional extensions may be registered on the HL7 FHIR registry at <http://hl7.org/fhir/registry>.


#### US Core Profile Extensions
The following extensions are used in US Core Profiles.
<!-- ================================================ -->
<!--  use this line to include an autogenerated list of all profiles and highlight new ones using the input/data/new_stuff.yml list.  Remove it if you would like to hand generate it -->
{% include ext-list-generator.md use="profile" %}
<!-- parameter values "ig"|"realm"|"profile" -->
<!-- ================================================ -->
#### Other US Realm Specific Extension
The following extensions are not used in any US Core Profile. They are provided to assist implementers who may find them relevant to their specific use cases.

{% include ext-list-generator.md use="realm" %}

#### US Core Profile StructureDefinition Extensions
The following extensions are only used in the in US Core Implementation Guide to created US Core Profiles. They are used in the context of StructureDefinition elements.

{% include ext-list-generator.md use="ig" %}

{% include link-list.md %}

<br />