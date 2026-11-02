# Changelog

* **v1.1.1**:
Added new documentation files to the repository (e.g., the `CITATION.cff` file) and refactored some components.
* **v1.1.0**: 
Added new documentation, including annotation properties (e.g., `bibo:doi`, `schema:codeRepository`, etc.), term properties (e.g., `vann:example`, `vs:term_status`, etc.), exemplary competency questions with their respective SPARQL queries, and a Grafoo diagram.
Added new named individuals `mito:explicit` and `mito:implicit` (previously only mentioned in documentation as `mito:ExplicitMention` and `mito:ImplicitMention`).
Specified that `mito:Mention` is a subclass of `sit:Situation` and, as a consequence, its properties as subproperties of `sit:isSettingFor`.
