# NifXML

**XML-based specification of the NetImmerse and Gamebryo NIF file formats.**

NifXML provides a structured, human-readable description of the NIF file format used by NetImmerse/Gamebryo-based games and tools. It documents binary file layouts, data types, object hierarchies, version-specific structures, and game-specific extensions to support file format research, reverse engineering, and game asset tooling.

This repository is a fork of the original [Niftools/NifXML](https://github.com/niftools/nifxml) project.

## Overview

The core of this repository is [`nif.xml`](nif.xml), a machine-readable format definition that can be used by applications and development tools to interpret NIF files. The specification also serves as a reference for developers investigating differences between engine and game versions.

NifXML is **a format specification, not a standalone NIF viewer, editor, or converter**. Applications built around the specification provide those capabilities.

## Features

- **Binary format definitions** — Descriptions of NIF headers, structures, fields, object types, and references.
- **Data type documentation** — Basic types, structured types, enumerations, bitflags, and object inheritance.
- **Version-aware layouts** — Conditions and metadata for differences across supported NIF versions and engine variants.
- **Game-specific extensions** — Definitions relevant to Bethesda titles and other games using NetImmerse or Gamebryo technology.
- **Tooling integration** — A shared source of format information for readers, writers, documentation tools, and reverse-engineering workflows.
- **HTML reference generation** — A Python script for building browsable format documentation from the XML definition.

Format coverage varies by version; a documented version or structure does not necessarily imply complete support in every consuming application.

## Repository Structure

```text
nifxml/
├── doc/          # Documentation assets and generated HTML output
├── tools/        # XML parsing and documentation support modules
├── nif.xml       # NIF file format specification
├── nifdoc.py     # HTML documentation generator
└── LICENSE       # GNU General Public License v3.0
```

## Getting Started

### Clone the repository

```bash
git clone https://github.com/thedragonheir/nifxml.git
cd nifxml
```

### Explore the format specification

Open [`nif.xml`](nif.xml) in a text editor to inspect the available definitions. Common elements include:

| Element | Purpose |
| --- | --- |
| `version` | Describes file-format versions and associated game variants. |
| `basic` | Defines primitive or special binary data types. |
| `enum` / `bitflags` | Defines named values and flag sets. |
| `struct` | Describes compound data structures and their fields. |
| `niobject` | Describes NIF object blocks and inheritance relationships. |
| `field` | Describes individual members, including type and conditional layout information. |

For example, the XML definition of a three-dimensional vector is:

```xml
<struct name="Vector3" size="12" module="NiMain">
    A vector in 3D space (x,y,z).
    <field name="x" type="float">First coordinate.</field>
    <field name="y" type="float">Second coordinate.</field>
    <field name="z" type="float">Third coordinate.</field>
</struct>
```

### Generate HTML documentation

The included `nifdoc.py` script generates linked HTML reference pages from the XML specification. From the repository root, run:

```bash
python nifdoc.py
```

The documentation is written to the `doc/` directory by default. Open `doc/index.html` in a browser to explore the generated object hierarchy and type reference.

To see the available command-line options:

```bash
python nifdoc.py --help
```

Options include changing the output location, omitting metadata columns, and filtering out definitions below a specified minimum version. The generator uses the Python support modules included in this repository.

## Related Projects

NifXML is part of the wider [Niftools](https://www.niftools.org/) ecosystem:

- **[NifSkope](https://github.com/niftools/nifskope)** — Viewer and editor for NIF game assets.
- **[Niflib](https://github.com/niftools/niflib)** — C++ library for reading and writing NIF files.
- **[PyFFI](https://github.com/niftools/pyffi)** — Python library for working with block-structured binary formats.
- **[Blender Niftools Addon](https://github.com/niftools/blender_niftools_addon)** — Blender integration for importing and exporting supported NIF-related assets.

These projects have different levels of format and version support; check each project's documentation for compatibility details.

## Contributing

Corrections to the format description are valuable, particularly when based on reproducible analysis of existing NIF files.

When proposing a change:

1. Identify the affected NIF version, game, and object or data type.
2. Explain the observed binary layout and how it differs from the current XML definition.
3. Update documentation and version conditions where appropriate.
4. Avoid changing layouts for unrelated versions without supporting evidence.

For changes intended to benefit the wider ecosystem, consider contributing them to the [upstream Niftools repository](https://github.com/niftools/nifxml).

## Documentation and Resources

- [Niftools project website](https://www.niftools.org/)
- [Original NifXML repository](https://github.com/niftools/nifxml)
- [NifXML wiki](https://github.com/niftools/nifxml/wiki)
- [NIF format reference](https://www.niftools.org/nifxml/)

## License

This project is distributed under the **GNU General Public License v3.0 (GPL-3.0)**. See the [`LICENSE`](LICENSE) file for details.

## Acknowledgments

NifXML originates from the **Niftools project** and the contributions of its maintainers and community. This fork preserves that attribution and builds on their work documenting the NetImmerse/Gamebryo formats.
