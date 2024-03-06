
### Introduction

Clinicians use various terms such as *assessments*, *scales*, *surveys*, and *screenings* to describe the tools and processes to collect health-related information for assessing a patient's health-related matter. US Cores uses the term *Screening and Assessments* for the process of recording responses and capturing assertions/determinations resulting from this process and these tools. This page documents how Screening and Assessments are used to identify various problems or health concerns and how US Core Profiles record Screenings and Assessments ranging from simple observations to complex structured evaluations.

With the addition of the USCDI v3 Health Status Assessments data <span class="bg-success" markdown="1">elements,</span><!-- new-content --> US Core <span class="bg-success" markdown="1"></span><!-- new-content --> expanded the guidance from an Social Determinant of Health (SDOH)-only focus to a general framework of Screenings and Assessments for all domains<span class="bg-success" markdown="1">, including the USCDI Data Elements</span><!-- new-content -->:

- Social Determinant of Health (SDOH)
- Functional Status
- Disability Status
- Mental/Cognitive Status
- <span class="bg-success" markdown="1">Physical Activity</span><!-- new-content -->
- <span class="bg-success" markdown="1">Alcohol Use</span><!-- new-content -->
- <span class="bg-success" markdown="1">Substance Use</span><!-- new-content -->

However, implementers **SHOULD** consider more constrained, domain-specific profiles derived from the US Core Profiles to meet the needs of their respective use cases.

The [Gravity Project] and its [SDOH Clinical Care] HL7 Implementation Guide address the screening process and related interventions to address Social Determinant of Health (SDOH). Those efforts helped guide US Core 5.0.1 updates to meet the [USCDI v2] SDOH data elements for Assessments, Goals, Interventions, and Problems/Health Concerns.

### Related Activities in Clinical Care

The figure below shows how screening and assessments lead to providing services for a patient.

- **Screening and Assessments**: [Screening and Assessment](#screening-and-assessments) are used to identify problems before delivering appropriate clinical care. The following US Core Profiles support capturing their responses:
    - [US Core Simple Observation Profile]
    - The [US Core Observation Screening Assessment Profile]
    - The [SDC Base Questionnaire]/[US Core QuestionnaireResponse Profile]
- **Problems/Health Concerns**: The identified health-related conditions (for example, homelessness or disability) are represented by:
  - [US Core Simple Observation Profile]
  - [US Core Condition Problems and Health Concerns Profile].
- **Interventions**:  The [US Core ServiceRequest Profile] communicates services offered to patients to address problems/health concerns. The [US Core Procedure Profile] can also record a completed service or intervention.
- **Goals**: Identifying and defining a future desired condition or change in condition (for example, Has adequate quality meals and snacks) is represented by [US Core Goal Profile].

<!-- {% raw %} {% include img.html img="screening_and_assessments.svg" caption="Screening and Assessment Activities" %} {% endraw %} -->

### Screening and Assessments

Screening and Assessments are used to identify various problems or health concerns. Their complexity ranges from simple observations to complex structured evaluations: 


- Clinician makes a simple observation - (for example, the patient states they are homeless)
- Clinician administers a survey to gather information (for example, the [Protocol for Responding to and Assessing Patients' Assets, Risks, and Experiences (PRAPARE) Survey])
- Clinician makes a "clinical judgment" based on an assessment tool. (for example, based on the PRAPARE survey, the patient has a lack of access to transportation)

The following guidance was developed after reviewing several functional status, disability status, mental/cognitive status, and SDOH screening and assessment tools.


#### Clinical Judgments

Whether based on simple observations or detailed assessments, clinicians may record clinical judgments as:
- a problem or health concern
- as observation

Local policies guide what is appropriate for the problem list versus an observation. For example, some clinics may consider social needs as sensitive information and not appropriate for the problem list.  Observations can contribute to the identification of future problems or health concerns and support service requests and procedures.

Every server that supports the USDCI Data Class "Health Status/Assessments":

-  **SHALL** support representing clinical judgments using [US Core Condition Problems and Health Concerns Profile] or [US Core Simple Observation Profile].  
-  When a *Simple Observation* or *Problem or Health Concern* is recorded based on a structured screening an assessment (see below), the *US Core Simple Observation Profile* **SHOULD** reference it using the `derivedFrom` element and the *US Core Condition Problems and Health Concerns Profile* using the `evidence.detail` element,


#### Structured Screening and Assessments

Screening and Assessments can be structured survey instruments consisting of questions with a variety of response including true/false, coded, textual, and  multiple choice.  Examples include PRAPARE, [APGAR score] and [PHQ-9]. US Core defines two ways to represent the questions and responses to these screening and assessment instruments:

- Observation: [US Core Observation Screening Assessment Profile]
- Questionnaire/QuestionnaireResponse: [SDC Base Questionnaire]/[US Core QuestionnaireResponse Profile]

Systems *SHOULD* support all three profiles for USDCI Data Class Health Status/Assessments.  The table below summarizes the differences in conformance requirements for these profiles between version 5.0.1 and 6.0.0 of US Core

US Core Profile|5.0.1|6.0.0
---|---|---
The US Core Observation Screening Assessment Profile|SHALL(US Core Observation SDOH Assessment Profile)|SHALL
SDC Base Questionnaire|undefined|SHOULD
US Core QuestionnaireResponse Profile|MAY|SHOULD
{:.grid}

The sections below provide additional guidance on when Observations and Questionnaire/QuestionnaireResponse can be used to represent the structured screenings and assessments.


##### US Core Observation Screening Assessment Profile


[US Core Observation Screening Assessment Profile] is defined to record observations from responses to screening tools and assessments used for any context (e.g., SDOH, functional status, etc.). Although systems can represent most questions and answers in healthcare assessments as FHIR Observations, it is only sometimes necessary and appropriate to represent all of them as Observations. Only relevant responses should be extracted as Observations. For example, depending on the use case and focus of the Assessment or Survey, patient demographic information may be recorded in the Patient resource instead of Observations. The observations can be grouped and nested to preserve the structure of screening or assessment instruments. The figure below illustrates the relationship between the Observation screening and assessments "panel" and the individual screening and assessment "item" Observations. Each box represents an Observation:

<!-- {% raw %} {% include img-med.html img="uscore-observation-assessment-structure.svg" caption="Relationship Between Screening Assessment Observations" %} {% endraw %} -->

Note that the panels can be nested to create additional groupings of responses. See the [US Core Observation Screening Assessment Profile] page for detailed documentation on how the observations are linked, examples, and search requirements.

###### Searching for Screening and Assessment Data

Unlike QuestionnaireResponse, When Observations are used to record set of Screening and Assessments responses, clients can query individual responses using the standard FHIR RESTful API search parameters  Below is a simple example of a FHIR RESTful search transaction on Observation to access a patient's SDOH assessment data

<!-- {% raw %} {% include examplebutton.html example="SDOH_search_transaction" b_title = "Click on Here To See Search Example" %} {% endraw %} -->

##### SDC Base Questionnaire/US Core QuestionnaireResponse Profile

Screening and assessment instruments may be represented as questionnaires including FHIR Questionnaires.  The [Structured Data Capture (SDC)] specification documents the workflow for the creation, discovery and retrieval and data-extraction of FHIR Questionnaire and QuestionnaireResponse. The [US Core QuestionnaireResponse Profile] is based on the [Structured Data Capture (SDC) Questionnaire Response Profile]), and is used to capture, exchange and persist the response data. QuestionnaireResponse can be thought of as a snapshot of the filled-out answer forms to the screening and assessment questions represented in the [SDC Base Questionnaire]. It is ordered and grouped corresponding to the Questionnaire and can be consulted when a complete and accurate record of the responses is required. the [US Core QuestionnaireResponse Profile] page for detailed documentation, examples and search requirements.

###### Extracting US Core Observation Screening Assessment from US Core QuestionnaireResponse

US Core Observation Screening Assessment can be extracted from US Core QuestionnaireResponse.  Although QuestionnaireResponse can be searched using the standard FHIR RESTful API search parameters, individual responses are not directly searchable in QuestionnaireResponse. In order to search directly for individual responses, the QuestionnaireResponse must be “parsed” into a searchable form - i.e. to a local FHIR or non-FHIR data store such as a database or FHIR Observations. Both SDC and the [SDOH Clinical Care] implementation guide define how data captured in a QuestionnaireResponse can be extracted and used to create or update Observations or other FHIR resources.



#### Choosing Between QuestionnaireResponse and Observation

For API developers using US Core, it's important to understand when to use the QuestionnaireResponse versus Observation to represent structured assessments and surveys. Here are some guidelines to help choose the appropriate profile:

- Observations represent specific point-in-time facts that need to be searched, trended, be the subject of statistical analysis and/or directly referenced in support of other actions.  Not all answers in a form will necessarily be appropriate to surface as an Observation.  However, anything that meets one of the preceding criteria will need to be surfaced as an Observation.
- QuestionnaireResponses represent the source-of-truth of a completed form.  QuestionnaireResponse shows how the question was phrased, what answer text was seen or typed, the order in which the survey or assessment was completed, etc. For FHIR implementers, it is important to note that QuestionnaireResponse references specific versions of a form filled out whether the form was represented as a FHIR Questionnaire or not. (however, it may be challenging to determine canonical URLs and linkIds that are consistent across systems without using a FHIR Questionnaire.) This reference provides the context of exactly what options were available to choose from, what logic was used to calculate answers, or to determine what questions were asked. It is important to note that QuestionnaireResponse cannot be used for searching based on individual responses but can be used to capture higher-level information such as what form was filled out, by whom, and when.

In many cases, data might be represented using both mechanisms - the initial raw assessment retained for audit or detailed review stored as a QuestionnaireResponse, and the detailed key answers surfaced as Observations for easy search and analysis.


### Terminology

#### Category Codes

API consumers may <span class="bg-success" markdown="1">query by category</span><!-- new-content --> (for example, `sdoh`) when accessing patient information. <span class="bg-success" markdown="1">Category codes for USCDI Health Assessments Data Elements are listed in the table below. They **SHOULD** be used when generating resources that conform to these profiles</span><!-- new-content -->:

- US Core Simple Observation Profile
- US Core Observation Screening Assessment Profile
- US Core Condition Problems and Health Concerns Profile
- US Core ServiceRequest Profile 

<div class="bg-success" markdown="1">

##### USCDI Health Assessments Data Element Category

{% include assessment-category-table-generator.html %}

</div><!-- new-content -->

Each profile's *Quick Start* section shows searches by category. Although not defined in US Core Procedure, implementers can categorize procedures using US Core Category or infer the context by inspecting the referenced ServiceRequest. Similarly, they can review the Questionnaire's metadata to determine US Core QuestionnaireResponse's context.


 <span class= "bg-warning" markdown= "1">Clients need to understand that data categorization is somewhat subjective. The categorization applied by the source may not align with the client's expectations. Clients may find it more beneficial to use queries based on a specific code or set of codes or to perform additional client-side filtering of query results.</span><!-- bg-warning -->

#### Screening and Assessment Codes

The US Core Observation Screening Assessment Profile, SDC Base Questionnaire, and US Core Simple Observation Profiles have [preferred] or [example] bindings to broadly defined LOINC value sets. These value sets contain concepts that span many use cases and are not bound to any USCDI Health Assessments Data Element.  

##### USCDI Health Assessments Data Element Value Sets

The following sections and table below identify the associated value sets for each USCDI Health Assessments Data Element.  This guidance intends to promote interoperability by introducing "starter" value sets *where available* for the USCDI Data Elements covered by Screenings and Assessments. These value sets are divided into clinical judgement codes and structured screening and assessment's panel and panel item codes.  Note that in several instances a suitable value set has not yet been identified. Implementers **SHOULD** treat these value sets as having an [extensible] binding. In other words, the *Clinical Judgement Codes* code sets are extensibly bound to the US Core Condition Problems and Health Concerns Profile the US Core Simple Observation Profile when representing clinical judgments. Similarly, *Panel Codes* and *Panel Item Codes* are extensibly bound to the US Core Observation Screening Assessment Profile and SDC Base Questionnaire/US Core QuestionnaireResponse Profile when representing structured screening and assessments. Because the value sets in this table are not formally bound to a US Core Profile in the StructureDefinitions, "automatic" validation (confirmation) that a code is a member of a value set will not occur using the standard validation tools.

###### SDOH value sets

- The Gravity project created and maintains the [Social Determinants of Health Screening Assessments And Questions](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1247.206/expansion) value set for the SDOH USCDI Health Assessments Data Element. This value set contains both panel and panel item codes.

   In addition to these concepts, implementers should consider using several SDOH value sets maintained and updated in VSAC by [Multiple Chronic Condition (MCC) Care Plan Implementation Guide] and the HL7 Patent Care work group with support from the National Institute of Health.  These are panel item codes that may part of a LOINC panel.
   
{% include mcc-valueset-list-generator.html %}

###### Functional Status

- The [Functional Status Related Questionnaire Panel Codes](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.1586/expansion) contains LOINC panel codes that represent functional status questionnaire LOINC panel code, such as CMS Assessment.

###### Mental and Cognitive Health

- The [Cognitive Health Related Questionnaire Panel Codes](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.979/expansion) contains LOINC panel codes that represent Mental or Cognitive health screening assessments, such as FACIT, PROMIS and MoCA.

- The [Cognitive Function Clinician Interpretation](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.979/expansion) represent clinical judgement codes such as, "Cognitive Function Interpretation".

- The [Mental Status Observation](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1240.1/expansion) value set contains SNOMED CT clinical judgement codes related to mental status observations that can come from a broad range of subjective and objective information such as Assessment and Screening tools. In many cases the value (answer) at Observation.value may be boolean true \| false.

###### Disability Status

- The [Disability Status Assessment](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1099.49/expansion) contains LOINC panel item codes that represent detailed patient questions about functional status, such as difficulty dressing or bathing.

###### Physical Activity

- The [Physical Activity Observation Questions](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1240.9/expansion) are panel item codes taken from the [Physical Activity Implementation Guide], sponsored by the [American Heart Association] and the [Physical Activity Alliance]. In addition to contributing to the terminology for the USCDI Health Assessments Physical Activity Data Element, the guide documents a standardized way of measuring and sharing a patient's physical activity.

   In addition to these concepts, implementers should consider using   [Physical Activity Level](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.1068/expansion) referenced in the SDOH section above. It represents simple question and answer assessment questions such as, "Kinds of physical activity you usually performed while on the job this last year" or "Days per week of moderate to vigorous physical activity".

###### Substance Use (Including Alcohol Use)

- The [Substance Use](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.1015/expansion) contain LOINC panel item codes such as, "How often do you have a drink containing alcohol" or "How often have you used any prescription medications just for the feeling, more than prescribed or that were not prescribed for you in past 12 months (TAPS)"

- The [Alcohol Use Related Questionnaire Panel Codes](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.1585/expansion) contains the LOINC Panel Codes for Alcohol Use Disorder Identification Test - Consumption AUDIT-C and PROMIS short form - alcohol - alcohol use 7a - version 1.0.

- The [Drug Misuse](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1222.707/expansion) values set contains SNOMED CT clinical judgement codes
to represent conclusions or diagnoses pertaining to drug misuse or abuse. In many cases the value (answer) at Observation.value may be boolean true \| false.

{% include assessment-valueset-table-generator.html %}

This information is also available as a [csv](assessments-valuesets.csv) or [excel](assessments-valuesets.xlsx) file:


#### Codes for Problems/HealthConcerns, Goals, Service Requests, and Procedures

US Core uses broadly defined value sets that contain concepts used across use cases, including SDOH. For the SDOH Clinical Care HL7 Implementation Guide, the Gravity Project has defined “Grouped Value Sets” across specific social risk factor domains for problems/health concerns, goals, procedures, and service requests. Value sets for each SDOH domain are bundled together to create the groupings. The links below are to these Gravity Project-managed value sets in [Value Set Authority Center (VSAC)]. In VSAC, clicking “Grouping Members” within the Value Set Details tab will present the many individual value sets in the group representing the various SDOH domains. These grouped value sets are narrower subsets of the value sets allowed in the respective US Core Profiles. However, when recording SDOH data US Core Profiles, servers **SHOULD** use them.

* [Social Determinants of Health Conditions Value Set](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1196.788/expansion)
* [Social Determinants of Health Procedures Value Set](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1196.789/expansion)
* [Social Determinants of Health Goals Value Set](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1247.71/expansion)
* [Social Determinants of Health Service Requests Value Set](https://vsac.nlm.nih.gov/valueset/2.16.840.1.113762.1.4.1196.790/expansion)

 The figure below illustrates how the Gravity value sets are grouped for use in the US Core Condition Problems and Health Concerns Profile and how the grouped value set is compatible with the broader US Core Problem code value set.

<!-- {% raw %} {% include img-med.html img="sdoh_condition.svg" caption="SDOH Grouped Value Set Reuse in US Core" %} {% endraw %} -->

### Examples

These are example instances that show what Screening and Assessments data produced and consumed by systems conforming with this implementation guide might look like.

{% include assessment_examples.md %}


{% include link-list.md %}
