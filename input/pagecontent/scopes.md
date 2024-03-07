
 SMART App Launch Implementation Guide Release 2.0.0 describes a set of foundational patterns based on OAuth 2.0 for client applications to authorize, authenticate, and integrate with FHIR-based data systems. This page  documents the SMART on FHIR obligations and capabilities for US Core Servers supporting User-Facing Applications and Backend Services. 

### *Capability Sets* for US Core Servers Supporting User-Facing Applications

To promote interoperability, SMART on FHIR defines a set of core capabilities. An individual SMART server will publish a granular list of its capabilities and a given set of these capabilities is combined to support a specific use, a *Capability Set*. See SMART App Launch's [FHIR OAuth authorization Endpoints and Capabilities](https://hl7.org/fhir/smart-app-launch/STU2/conformance.html#smart-on-fhir-oauth-authorization-endpoints-and-capabilities) for more details.

The following SMART on FHIR *Capability Sets* **SHALL** be supported for US Core Servers that support User-Facing Applications:

- [Patient Access for Standalone Apps](https://hl7.org/fhir/smart-app-launch/STU2/conformance.html#patient-access-for-standalone-apps)
- [Clinician Access for EHR Launch](https://hl7.org/fhir/smart-app-launch/STU2/conformance.html#clinician-access-for-standalone)

🤔 at least one or both? ( see CCG reference below )

🤔 SHOULD there be a *Capability Sets* recommendation for "Backend-Services"?

Servers **MAY** support the other SMART on FHIR *Capability Sets*.

🤔 what about listing individual capabilities  - I do not think this section in HTI-1 Section III 7 e means that *all* US Core Servers **SHALL** support *all* the capabilities in section 8.1.2.
> As part of this proposal, we proposed to adopt several sections specified as “optional” in the SMART v2 Guide as “required” for purposes of the Program for certification criteria that reference § 170.215(c). Specifically, we proposed to adopt all Capabilities as defined in “8.1.2 Capabilities,” which include but are not limited to (1) backward compatibility mapping for SMART v1 scopes as defined in “3.0.2 Scopes for requesting clinical data;” (2) asymmetric client authentication as defined in “5 Client Authentication: Asymmetric (public key);” and granular scopes as defined in (3) “3.0.2.3 Finer-grained resource constraints using search parameters.”
 - review of [ONC Certification Companion Guides (CCGs)]( https://www.healthit.gov/test-method/standardized-api-patient-and-population-services) (Updated on 02-20-2024)

    >Paragraph (g)(10)(v)(A)(1)
    > - Health IT Modules will only be tested for the "Patient Access for Standalone Apps" and "Clinician Access for EHR Launch" "Capability Sets”described in the standard adopted at § 170.215(a)(3)
    >   - § 170.215(a)(3) HL7 SMART Application Launch Framework Implementation Guide Release 1.0.0, including mandatory support for the “SMART Core Capabilities” (incorporated by reference in § 170.299).


### US Core Servers SHALL Support Token Introspection

US Core Server **SHALL** support token introspection defined by the SMART App Launch Guide. For more details and additional consideration see SMART App Launch's [Token Introspection](hhttps://hl7.org/fhir/smart-app-launch/STU2/token-introspection.html#token-introspection).

### SMART Scopes


SMART’s scopes defined in Version 2.0.0 of the [SMART App Launch] implementation guide allow a access permissions to be delegated to a client application. The US Core API requires servers to support [resource level scopes] and [granular scopes] allowing access to specific data about a single patient. US Core's required scopes (**SHALL**) are based on community-based consensus that the scope meets a system requirement, clinical need, or federal regulation. Similarly, US Core's recommended scopes (**SHOULD**) rely on community-based consensus that the scope meets a system requirement or clinical need as a best practice.

The US Core required scopes listed below are named in the HTA-1 final rule, which requires support for Condition and Observation category scopes, and the recommended granular scope listed below is of particular interest to patients and health systems.

US Core clients should follow the [principle of least privilege] and access only the necessary resources. In other words, if a client needs only vital sign observations, it should request access only to Observations with a category of "vital-signs".

##### Scopes Format
 SMART App Launch Version 2.0.0 introduced a scope syntax of: `<patient|user|system> / <fhir-resource>. <c | r | u | d |s> [?param=value]`

For example, to limit read and search access to a specific patient's laboratory observations but not other observations, the server grants the following patient-specific scope:

`patient/Observation.rs?category=http://terminology.hl7.org/CodeSystem/observation-category|laboratory`.

This example uses a `patient/` prefix, but implementers may support `system/` and `user/`.

#### US Core Scopes

The table below summarizes the US Core scope requirements (**SHALL**) and best practice recommendations (**SHOULD**) for resource-level and granular scopes. This same information can be found in each US Core Profile page's "Quick Start" section.

 A system's support for patient-level (`patient`), user-level (`user`) , and system-level (`system`) scopes depends on its published list of SMART on FHIR capabilities.  For example, if a server lists `permission-patient` and `permission-user` in its capabilities, it **SHALL** support both patient-level and user-level required scopes, and **SHOULD** support both patient-level and user-level recommended best-practice scopes

##### The Following Resource Level Scopes **SHALL** Be Supported


{% include resource-scopes-table.md conformance="SHALL" crud='rs'%}

<table class="grid">
<thead>
<tr>
<th>Resource Type</th>
<th>Resource Level Scope</th>
</tr>
</thead>
<tbody>
{% for resource_scope in resource_scopes -%}
<tr>
<td>{{resource_scope}}</td>
<td><code>{{ resource_scope | prepend: '<patient|user|system>/' | append: '.rs' }}</code></td>
</tr>
{% endfor %}
</tbody>
</table>

##### The Following Granular Scopes **SHALL** Be Supported

{% include granular-scopes-table.md conformance="SHALL" crud='rs' %}

<table class="grid">
<thead>
<tr>
<th>Resource Type</th>
<th>Granular Scope</th>
</tr>
</thead>
<tbody>
{% for granular_scope in granular_scopes -%}
<tr>
<td>{{granular_scope | split: '.' | first }}</td>
<td><code>{{ granular_scope | prepend: '<patient|user|system>/' }}</code></td>
</tr>
{% endfor %}
</tbody>
</table>

##### The Following Granular Scopes **SHOULD** Be Supported

{% include granular-scopes-table.md conformance="SHOULD" crud ='rs' %}

<table class="grid">
<thead>
<tr>
<th>Resource Type</th>
<th>Granular Scope</th>
</tr>
</thead>
<tbody>
{% for granular_scope in granular_scopes -%}
<tr>
<td>{{granular_scope | split: '.' | first }}</td>
<td><code>{{ granular_scope | prepend: '<patient|user|system>/' }}</code></td>
</tr>
{% endfor %}
</tbody>
</table>

### Servers SHALL support the following metadata in their `/.well-known/smart-configuration`

In addition to the capabilities defined in the server's CapabilityStatement, servers **SHALL** document their SMART capabilities in a using a [Well-Known Uniform Resource Identifiers (URIs)](https://hl7.org/fhir/smart-app-launch/STU2/conformance.html#using-well-known) JSON file.

#### Required SMART App Launch Metadata

The following JSON file metadata are required by the SMART App Launch guide:

- `issuer` (conditional)
- `jwks_uri` (conditional)
- `authorization_endpoint`
- `grant_types_supported`
- `token_endpoint`
- `capabilities`
- `code_challenge_methods_supported`

#### Additional US Core Requirements

These additional SMART App Launch metadata are required by US Core:

- `scopes_supported` : Array of scopes a client may request.
    - The server **SHALL** support all scopes listed in the table above for the US Core Profiles they support; additional scopes **MAY** be supported (so clients should not consider this an exhaustive list). 

    - Servers **MAY** limit clients' scopes to those configured at registration time. Servers **SHALL** allow users to select a subset of the requested scopes at the approval time. The app **SHOULD** inspect the returned scopes and accommodate the differences from the scopes it requested and registered.
- `introspection_endpoint`: URL to a server’s introspection endpoint that can be used to validate a token. 
  - Servers **SHALL** document this endpoint in the file

#### Example `.well-known/smart-configuration` File

This example `.well-known/smart-configuration` file shows all the required and recommended metadata listed in SMART App Launch. Note that the server lists `permission-patient` and `permission-user` in the `capabilities` metadata array and all the required and recommended US Core scopes for both `patient/` and `user/` in the `scopes_supported` metedata array.  See the [SMART App Launch] Implementation Guide for more examples and details.

~~~http
HTTP/1.1 200 OK
Content-Type: application/json
~~~

{% include granular-scopes-table.md %}

~~~json
{
  "issuer": "https://ehr.example.com",
  "jwks_uri": "https://ehr.example.com/.well-known/jwks.json",
  "authorization_endpoint": "https://ehr.example.com/auth/authorize",
  "token_endpoint": "https://ehr.example.com/auth/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_basic",
    "private_key_jwt"
  ],
  "grant_types_supported": [
    "authorization_code",
    "client_credentials"
  ],
  "registration_endpoint": "https://ehr.example.com/auth/register",
  "scopes_supported": [
    "openid",
    "profile",
    "launch",
    "launch/patient",
    "offline_access",
{% for resource_scope in resource_scopes -%}
    {{ resource_scope | prepend: '    "patient/'| append: '.rs' }}",
{{ resource_scope | prepend: '    "user/'| append: '.rs' }}",
{% endfor -%}
{% for granular_scope in granular_scopes -%}
    {{ granular_scope | prepend: '    "patient/'}}",
{{ granular_scope | prepend: '    "user/'}}"{% unless forloop.last %},{% endunless %}
{% endfor -%}
  ],
  "response_types_supported": ["code"],
  "management_endpoint": "https://ehr.example.com/user/manage",
  "introspection_endpoint": "https://ehr.example.com/user/introspect",
  "revocation_endpoint": "https://ehr.example.com/user/revoke",
  "code_challenge_methods_supported": ["S256"],
  "capabilities": [
    "launch-ehr",
    "permission-patient",
    "permission-user",
    "permission-v2",
    "client-public",
    "client-confidential-symmetric",
    "context-ehr-patient",
    "sso-openid-connect"
  ]
}
~~~
 

{% include link-list.md %}




