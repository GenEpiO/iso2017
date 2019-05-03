The GenEpiO/iso2017 repository offers a choice of formats for downloading the ontology terms referenced in the draft working document ISO/TC 34/SC 9 N 000 "Microbiology of the Food Chain — Whole Genome Sequencing, Typing and Genomic Characterization of Foodborne Bacteria". All formats include the label and definition of each term mentioned in a specification, as well as numeric and textual field constraints.  An example form rendering of the GenEpiO/iso2017 specification is available for Chrome browsers by visiting http://genepio.org/geem/form.html#GENEPIO:0002083 . The ontology identifier GENEPIO:0002083 points to GenEpiO term "draft sequence repository contextual data standard", which is a term under which the following components and their terms and selection lists are organized:

* Laboratory Contact Information
* Sample Collection
* Isolate
* Isolate Passage History
* Food Specimen
* Antibiogram
* Sequencing
* Sequence Assembly Quality Metrics

The plain-text **.tsv** (tabular) format options may be the most accessible for software developers as they have the simplest structure.  

* **iso_form_core_nodes.tsv** : The "core" nodes file contains all field terms in a specification, except for the underlying choices of categorical input fields.  
* **iso_form_core_edges.tsv** : Relations between a parent specification element and its underlings are specified here.
* **iso_form_all_nodes.tsv** : Includes core nodes, but also has all underlying categorical choices.
* **iso_form_all_edges.tsv** : Includes core edges, but also has all relations that define categorical lists and hierarchies. 

Note that a nodes table can list a particular ontology term more than once - for example on a form the same country list may occur for both sample location and sample collection agency location.  The "GEEM all edges .tsv" file will repeat both form fields' choices in full.  Also note that some categorical pick-list fields have a "lookup" user interface feature set. This is set in the GEEM raw specification in the case where a field's selections are too large or unwieldy to include directly in a form (for example, listing all the municipalities in the world as possible sample sites to pick from). The lookup feature indicates that further choices can be fetched from online ontology lookup services like OLS; however implementers may want to include their own cacheable term lookup system for such functionality. Currently this feature is not listed in the core/all nodes tables.

Columns in a **nodes.tsv** file's table:

* **datatype**: One of the XML schema datatypes allowable under OWL, or "model", which indicates a grouping of form fields. The xmls:anyURI datatype indicates that given item is a categorical variable or an underlying choice of one.
* **path**: Forward slash / delimited list of form parts between top level form and given term or component. This is a full path rather than just a parent identifier to avoid ambiguity in the situation where a form field or component appears in more than one form section.
* **id**: Ontology_id of term or component
* **label**: label of term as source ontology defines it
* **definition**: definition of term as source ontology defines it
* **ui_label**: User interface label of term, which can be provided if use of ontology defined label is awkward.
* **ui_definition**: User interface definition for term, provided when ontology definition is more focused on formal logic description for example.
* **help**: User interface help about term.
* **minValue**: For a numeric variable, minimum value constraint
* **maxValue**: For a numeric variable, maximum value constraint
* **minLength**: For a string variable, minimum string length constraint
* **maxLength**: For a string variable, maximum string length constraint
* **pattern**: A keyword like "email" that describes a pre-defined string format, or a regular expression constraining a textual or numeric field entry.
* **format**: E.g. "dateFormat:ISO 8601" enables specification of predefined formats.
* **preferred_unit**: If a field has more than one unit choice, this indicates the preferred unit.

Columns in an **edges.tsv** file's table:

* **relation**: Type of relation existing between parent and child, e.g. "component", or "choice"
* **path**: parent term (or component) identifier, including path to that parent.
* **child_id**: child term (or component) identifier.
* **minCardinality**: The minimum number of the child type of field or component allowed to exist under parent.
* **maxCardinality**: The maximum number of the child type of field or component allowed to exist under parent. For example, enables one to specify up to 3 phone numbers.

The **iso_form.json** (and Yaml) format is a hierarchic data structure whose elements represent form sections and fields, in order.  Hierarchic categorical picklists are represented as ordered dictionaries within dictionaries, recursively. This format also includes synonyms for terms.

* **iso_form.json**
* **iso_form.yaml**

The **iso_raw.json** (and Yaml) format is in the relatively flat format that is used to drive the "GEEM" form renderer referenced above. Each ontology term, including units, gets a single top-level entry, so this format has the smallest file size. The hierarchy of elements in the specification are constructed from a given term id (in this case GENEPIO:0002083) by looking at that term's components and choices (in case of categorical variable fields).

* **iso_raw.json**
* **iso_raw.yaml**

Lastly, the **genepio-merged.owl** file is the GenEpiO ontology file that was used to generate the ISO specification formats above. This file however contains many other ontology terms besides those included in the specification.
