- {{include.recommendation}} The `Observation.category` element provides an efficient way of restricting search on observations to a given context such as {{include.category | append: ' observations'}}. Example searches are shown in the [Quick Start](#search) section below. However, clients need to understand that data categorization is somewhat subjective. The categorization applied by the source may not align with the client's expectations. Clients may find it more useful to use queries based on a specific code or set of codes or to perform additional client side filtering of query results.