{% include StructureDefinition-us-core-vital-signs-notes.md code2="85354-9" code3="96607-7" %}

<div class="bg-success" markdown="1">

1. **SHOULD** support searching using  **[`patient`](SearchParameter-us-core-observation-patient.html)** and **[`code`](SearchParameter-us-core-observation-code.html)** and **[`_lastUpdated`](SearchParameter-us-core-observation-date.html)** search parameters:
    - including optional support for *OR* search on `code` (e.g.`code={system|}[code],{system|}[code],...`)
    - including support for these `date` comparators: `gt,lt,ge,le`
    - including optional support for *AND* search on `date` (e.g.`date=[date]&date=[date]]&...`)

    `GET [base]/Observation?patient={Type/}[id]&code={system|}[code]{,{system|}[code],...}&_lastUpdated={gt|lt|ge|le}[date]{&date={gt|lt|ge|le}[date]&...}`

    Example:
    
      1. GET [base]/Observation?patient=1186747&amp;code={{code1}},{{code2}},{{code3}}&amp;_lastUpdated=ge2024-03-19

    *Implementation Notes:* Fetches a bundle of all Observation resources for the specified patient and code(s) based on ***the last time they were changed***. **SHOULD** support search by multiple codes. ([how to search by reference] and [how to search by token] and [how to search by date]. ***See the [General Guidance](guidance.html#searching-using-lastupdated) section for additional guidance on searching using `_lastUpdated`.***)
</div><!-- new-content -->

{% include link-list.md %}
