### US Core Conformance Artifacts:

### Conforming to US Core

### Using Codes in US Core Profiles

#### Extensible Binding for Coded Elements

[Extensible Binding]  means that one of the codes from the specified ValueSet **SHALL** be used if an applicable concept is present.  If no suitable code exists in the ValueSet, alternate code(s) may be provided.  For `CodeableConcept`, which permits multiple codings and a text element, this rule applies to *at least* one of the codings, and if only text is available and <span class="bg-success" markdown="1">it has no conceptual overlap to the bound coded values</span><!-- new-content -->, then just text may be used.

The [US Core AllergyIntolerance Profile] illustrates the extensible binding rules for CodeableConcept datatype.  The `AllergyIntolerance.code` element has an extensible binding to the VSAC ValueSet "Common substances for allergy and intolerance documentation including refutations" Allergy. When claiming conformance to this profile:

- US Core Responders **SHALL** provide:
  - a code from this valueset in `AllergyIntolerance.code.code` *if the concept exists* in the ValueSet
  - or an alternative code <span class="bg-success" markdown="1">or text in `AllergyIntolerance.code. text'</span><!-- new-content --> *if the concept does not exist* in the ValueSet
- US Core Requestors **SHALL** be capable of processing the code in `AllergyIntolerance.code.code` or text in `AllergyIntolerance.code.text`

  {% include img.html img="Must_Support_AllergyIntolerance_code.png" caption="Figure 3: US Core AllergyIntolerance.code" %}

#### Current Binding for Coded Elements

The FHIR guidance for extensible bindings indicates that *all conceptual overlaps* including free text, be mapped to the coded values in the bindings. US Core adopts the [current] additional binding from FHIR R5 for more flexibility for exchanging legacy and text-only data. However, for newly recorded, non-legacy data, a system **SHALL** adhere to the extensible binding rules.

For example, the [US Core Procedure Codes] and  [US Core Condition Codes] ValueSets completely cover the domain. For data not captured by  fine-grained code it is possible to provide a a high-level abstract code*, such as SNOMED CT "Procedure". Therefore instead of requiring all legacy and text data be mapped to a standard code, the valueset uses a "current" binding

<span class="stu-note" markdown="1">

The "current" binding corresponds to the UC Core's interpretation of extensible bindings US Core version 6.1.0 and earlier.</span><!-- stu-note -->

  {% include img.html img="Must_Support_Condition_code.png" caption="Figure 4: US Core Condition.code" %}


### Using multiple codes with CodeableConcept Datatype

### Modifier Elements

### Missing Data

### FHIR RESTful Search API Requirements

### Search for Servers Requiring Status

{% include link-list.md %}