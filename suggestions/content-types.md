# Content types

An AsciiDoc file that is tested using Vale is typically either an assembly or a module. Both assemblies and modules must have a defined _content type_ to fit the templates and to be ready for DITA conversion. The content type must be defined as the `_mod-docs-content-type` attribute close to the start of the file, ideally on the first line (possibly excluding comment lines).

The content type of an assembly is always `assembly`. For modules, three content types are available:

* `concept`
* `reference`
* `procedure`

## assembly

For an assembly, the content type is always `assembly`:

```
`:_mod-docs-content-type: assembly`
```

The assembly typically has `include` directives to include modules. Most content is normally in modules, but there can be some content in an assembly too. The assembly can unclude subsections at any level, though more often the subsection titles are inside modules.

Assemblies use the `[leveloffset=+N]` setting to nest include modules, for example:

```
include:modules/head_module.adoc[leveloffset=+1]
include:modules/subsection_module.adoc[leveloffset=+2]
```

In this example, the content of `subsection_module.adoc` appears as a subsection under the content of `head_module.adoc`.

There is a [template for assemblies](https://raw.githubusercontent.com/redhat-documentation/modular-docs/refs/heads/main/modular-docs-manual/files/TEMPLATE_ASSEMBLY_a-collection-of-modules.adoc) , but all its parts except the context definition are optional, while absence the context definition does not necessarily affect DITA conversion. So an assembly "not conforming to the template" is usually not an issue.


An assembly file normally has "assembly" in its name and a `:mod-docs-content-type: assembly` attribute definition at the start of the file.

Every AsciiDoc module must has a _content type_ of `concept`, `reference`, or `task`.

## concept

A concept module corresponds to the DITA topic type `concept`. A concept module gives the user descriptions and explanations needed to understand and use a product. In other words, concepts provide background information that users must know before they can successfully work with a product or interface.

Usually, the structure of a concept is fairly simple, However, one level of subsections (level 2 headings, `==` prefix) is allowed in concepts.

The content type definition must be present close to the start of the file, ideally on the first line:

```
`:_mod-docs-content-type: concept`
```

There is a [template for concepts](https://raw.githubusercontent.com/redhat-documentation/modular-docs/refs/heads/main/modular-docs-manual/files/TEMPLATE_CONCEPT_concept-explanation.adoc) . but all its parts except the context definition are optional, while absence the context definition does not affect DITA conversion. So a concept "not conforming to the template" is usually not an issue, as long as no third-level subheadings (`===` prefix) nor deeper-level subheadings are present.

## reference

A reference module corresponds to the DITA topic type `reference`. A reference module provides data that users might want to look up, but do not need to remember. A reference module often includes lists and/or tables. A well-organized reference module enables users to scan the content quickly to find the details they want. Examples of reference modules include language elements, class descriptions, configuration parameter desctri[tions, commands, functions, statements, protocols, types, declarators, operands, and API information, which provide quick access to facts. Ideally, a reference module does not include no explanation of concepts or procedures. Concepts should be placed in concept modules and procedures should be placed in procedure modules.

One level of subsections (level 2 headings, `==` prefix) is allowed in references.

The content type definition must be present close to the start of the file, ideally on the first line:

```
`:_mod-docs-content-type: reference`
```

There is a [template for references](https://raw.githubusercontent.com/redhat-documentation/modular-docs/refs/heads/main/modular-docs-manual/files/TEMPLATE_REFERENCE_reference-material.adoc) . but all its parts except the context definition are optional, while absence the context definition does not affect DITA conversion. So a reference "not conforming to the template" is usually not an issue, as long as no third-level subheadings (`===` prefix) nor deeper-level subheadings are present.

## procedure

A procedure module corresponds to the DITA topic type `task`. A procedure module provides step-by-step instructions that enable a user to perform a task.

The content type definition must be present close to the start of the file, ideally on the first line:

```
`:_mod-docs-content-type: procedure`
```

Like the strict DITA `task` topic, a procedure module has a strict structure. No subheadings and no subsections are allowed. To denote the structural parts of a procedure, a procedure module uses block titles (`.Block title` AsciiDoc markup).

The [template for procedures](https://raw.githubusercontent.com/redhat-documentation/modular-docs/refs/heads/main/modular-docs-manual/files/TEMPLATE_PROCEDURE_doing-one-procedure.adoc) defines the complete list of block titles that are permitted in procedures and the strict structure of each part.

**Every procedure module mus strictly comply with the template to enable DITA conversion** . (One exception is the `{context}` part of the module ID, which is defined in the template but can be absent in a module).

If you create a new procedure module or split an existing module and one of the resulting modules is a procedure, ensure that the module complies with the template.

If the content of the module is factually a procedure, but it is not currently possible to rewrite it as a set of steps in the timeframe expected for the DITA conversion, a _last resort_ solution is to mark the module as a reference. **Such a decision musy not be taken lightly**
