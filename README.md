# RF2-to-OWL

This is a perl script to convert an International Edition RF2 package to OWL XML/RDF format. It has previously been distributed within the International Edition of SNOMED CT, but is now being made available under an Apache v2 license with the SNOMEd International GitHub repositories.

It has currently been tested by SNOMED International with the International Edition of SNOMED CT, and cannot be guaranteed to work with otnher editions or extensions of SNOMED CT.

## Running the script

Run the script as `perl <scriptfilename> <arg0> <arg1>` where `<scriptfilename>` is the name of the file containing this script `<arg0>` can be KRSS, OWL, or OWLF:

- **KRSS**: This produces KRSS2 which is parsable by the OWL API 3.4.2, or by CEL or other classifiers
- **OWL**: This produces the OWL XML/RDF format.
- **OWLF**: This produces the OWL functional syntax, parsable by the OWL API 3.4.2

`<arg1>` is the directory containing the RF2 Snapshot subdirectories.

If the current directory is RF2/Snapshot, then just use dot (".") to designate the current directory, as in the following example:

`perl tls2_StatedRelationshipsToOwlKRSS_Script_INT.pl OWLF .`

Alternatively you can separately supply arguments for all the file names (with their directories if necessary) : Run the script as `perl <scriptfilename> <arg0> <arg1> <arg2> <arg3> <arg4> <arg5> <arg6>` where

- `<scriptfilename>` is the name of the file containing this script
- `<arg0>` can be KRSS, OWL, or OWLF:

  - **KRSS**: This produces KRSS2 which is parsable by the OWL API 3.4.2, or by CEL or other classifiers
  - **OWL**: This produces the OWL XML/RDF format.
  - **OWLF**: This produces the OWL functional syntax, parsable by the OWL API 3.4.2

- `<arg1>` is the name of the file containing the SNOMED CT RF2 Concepts Table snapshot e.g. sct2_Concept_Snapshot_INT_20150131.txt
- `<arg2>` is the name of the file containing the SNOMED CT RF2 Descriptions Table snapshot e.g. sct2_Description_Snapshot_INT_20150131.txt
- `<arg3>` is the name of the file containing the SNOMED CT RF2 Stated Relationships Table snapshot, e.g. sct2_StatedRelationship_Snapshot_INT_20150131.txt
- `<arg4>` is the name of the file containing the SNOMED CT RF2 Text Definitions Table snapshot, e.g. sct2_TextDefinition_Snapshot-en_INT_20150131.txt
- `<arg5>` is the name of the file containing the SNOMED CT RF2 Language Refset snapshot, e.g. der2_cRefset_LanguageSnapshot-en_INT_20150131.txt
- `<arg6>` is the name of the output file, which is your choice but could be something like res_StatedOWLF_Core_INT_20150131.owl

It outputs a description logic representation, using either OWL or KRSS syntax.

**KRSS Notes**

The KRSS uses "define-primitive-concept" instead of the contracted "defprimconcept", and "define-concept" instead of the contracted "defconcept", and "define-primitive-role" instead of the contracted "defprimrole".

**OWL Notes**

The OWL syntax can be either RDF/XML or OWL Functional Syntax. The OWL sublanguage used (OWL 2 profile) is OWL 2 EL. The output files can be imported into an editor such as Protege using the OWL API.

The script relies on the hierarchy under 410662002 "Concept model attribute" to specify the role hierarchies.

The output consists of:

1. A set of role definitions
2. A set of concept definitions.

## Useful information

- **URI**: This version uses the URI specification adopted by IHTSDO. Components with an sctid are identified by: <http://snomed.info/id/{sctid}>
- **Preferred terms and synonyms** are identified by annotation properties according to an extension to the SNOMED CT URI Specification: original specification is: `http://snomed.info/field/{tableName}.{fieldName}`
- Identification of a Preferred Term requires two files and thus two tables, so this structure is inadequate to represent the combination of information from the Description table and the Language Refset table. The current script uses the following form, as an arbitrary extension of the specification: `http://snomed.info/field/{tableName}.{fieldName}.{language-dialect}.{preferred|synonym}`
- The annotation property for a US English Preferred term is: `http://snomed.info/field/Description.term.en-us.preferred` denoting that this is from the Description file, the term field, and in the US English language refset it is marked with acceptability = preferred. The annotation property for text definitions is `http://snomed.info/field/TextDefinition.term`

- Version 6.3, Date: 2016-02-09, Author: Yongsheng Gao, updated copyright and introduced variables for release version.

- Version 6.2, Date: 2014-11-21, Author: Kent Spackman

_OWL API VERSION COMPATIBILITY NOTE_: The version of OWL Functional Syntax is that required by OWL API 3.4.2

_Tested with OWL API version 3.4.2 in Protege 4.3._
