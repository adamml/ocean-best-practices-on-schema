# Schema.org implementation pattern for the Ocean Best Practices Repository

- **Author:** Adam Leadbetter, Marine Institute, Ireland
- **Version:** 1.0
- **Date:** 16th June 2020

## Contents

1. [Base type](#base-type)
1. [Metadata field mapping](#metadata-field-mapping)
1. [@id](#id)
1. [Title](#title)
1. [Authors and Maintainers](#authors-and-maintainers)
1. [Publisher](#publisher)
1. [Keywords](#keywords)
1. [Identifiers](#identifiers)
1. [Subjects](#subjects)
1. [Example](#example)
1. [Version history](#version-history)

## Base type
The base type chosen from the `Schema.org` vocabulary to represent a Best Practices document within the Ocean Best Practices Repository is [`CreativeWork`](https://schema.org/CreativeWork). From the Schema.org documentation, this base type represents `the most generic kind of creative work, including books, movies, photographs, software programs, etc.`.

![Base type diagram for representing entries in the Ocean Best Practices repository as Schema.org `CreativeWork` instances](./img/obpsAsSchema_01_overview.png)

## Metadata field mapping

Digging into the DSpace implementation of the repository, reveals a rich metadata model based on the Dublin Core mtadata terms. The following table shows a mapping from Dublin Core to appropiate Schema.org attributes, within the domain of the type of `CreativeWork`.

| **Dublin Core** | **_Schema.org attribute_** | **_Range of Schema.org attribute_** |
|---|---|---|
| **dc.contributor.author** | _author_ | Person |
| **dc.coverage.spatial** | _spatial_ | Place |
| **dc.date.accessioned** | | |
| **dc.date.available** | _datePublished_| Date |
| **dc.date.issued** | | |
| **dc.identifier.citation** | _identifier_ | PropertyValue |
| **dc.identifier.doi** | _identifier_ | PropertyValue |
| **dc.identifier.uri** | _identifier_ | PropertyValue |
| **dc.description.abstract** |  _abstract_ | Text |
| **dc.description.sponsorship** | _funder_ | Organization |
| **dc.language.iso** | _inLanguage_ | Language |
| **dc.publisher** | _publisher_ | Organization |
| **dc.relation.uri** | _sameAs_ | URL |
| **dc.rights** | _license_ | CreativeWork |
| **dc.rights.uri** | _license_ | CreativeWork |
| **dc.title** |_name_ | Text |
| **dc.type** | _genre_ | Text |
| **dc.description.status** | | |
| **dc.format.pages** | _numberOfPages_ - _*Strictly only on type Book. As is this flags as a 'warning' in Google's Structured Data Testing Tool. We could request an additional domian from Schema.org to make this 100%*_| Integer |
| **dc.description.refereed** |  | |
| **dc.publisher.place** | _publisher_ | Organization |
| **dc.subject.parameterDiscipline** | _about_, _keywords_ | ?, Text |
| **dc.subject.instrumentType** | _about_, _keywords_ | ?, Text |
| **dc.subject.dmProcesses** | _about_, _keywords_ | ?, Text |
| **dc.subject.other** | _about_, _keywords_ | |
| **dc.description.currentStatus** | | |
| **dc.description.contactemail** | _maintainer_ | Person |
| **dc.description.contactname** | _maintainer_ | Person |
| **dc.description.sdg** | _about_, _keywords_ | ?, Text|
| **dc.description.eov** | _about_, _keywords_ | ?, Text |
| **dc.description.bptype** | _about_, _keywords_ | ?, Text |
| **dc.description.maturitylevel** | _about_, _keywords_ | ?, Text |
| **dc.description.bptype** | _about_, _keywords_ | ?, Text |

The DSpace record also contains links to a number of files, which are mapped through the `hasPart` attribute.

## @id

The `@id` attribute of a `JSON-LD` encoding, such as is used in `Schema.org` is used to give the canonical Uniform Resource Identifier to the resource being described. As the Ocean Best Practices Repository uses the handle system, these persistent identifiers should be used in the `@id` attribute:

```json
{
	"@context": {"@vocab": "https://schema.org/"},
	"@type": "CreativeWork",
	"@id": "http://hdl.handle.net/11329/424"
}
```

## Title

The `name` attribute in `Schema.org`

```json
{
	"@context": {"@vocab": "https://schema.org/"},
	"@type": "CreativeWork",
	"name": "Schema.org implementation pattern for the Ocean Best Practices Repository"
}
```

## Authors and Maintainers

The [`Schema.org/author`](https://schema.org/author) attribute assigns a [`Person`](https://schema.org/Person) or [`Organization`](https://schema.org/Organization) responsible for the creation of a `CreativeWork` to that entity. 

![The use of `Schema.org/Person` for instances of `author` and `maintainer`](./img/obpsAsSchema_02_person.png)

For example:

```json
{
	"@context": {"@vocab": "https://schema.org/"},
	"@type": "CreativeWork",
	"author": [{"@type": "Person", "familyName": "Leadbetter", "givenName": "Adam"}]
}
```

**The use of ORCIDs would help to disambiguate these instances of `Person` and would reduce the size of the knowledge graph if the Schema.org serialization was ingested into a triple store.**

The [`Schema.org/maintainer`](https://schema.org/maintainer) attribute assigns a [`Person`](https://schema.org/Person) or [`Organization`](https://schema.org/Organization) responsible for the `manages contributions to, and/or publication of` the resource. This well describes the DCAT contact, for example:

```json
{
	"@context": {"@vocab": "https://schema.org/"},
	"@type": "CreativeWork",
	"author": [{"@type": "Person", "familyName": "Leadbetter", "givenName": "Adam", "email": "adam.leadbetter@marine.ie"}]
}
```

## Publisher

## Keywords

The [`keywords`](https://schema.org/keywords) attribute provides only an unstructured list of plain text keywords, which is why its use here is supplemented in the section on [Subjects](#subjects), which allow a richer description of the keywords to be developed. For example:

```json
{
	"@context": {"@vocab": "https://schema.org/"},
	"@type": "CreativeWork",
	"keywords": ["Parameter Discipline::Biological oceanography::Macroalgae and seagrass", "Parameter Discipline::Biological oceanography::Phytoplankton", "Phytoplankton biomass and diversity", "Sea surface temperature", "Ocean colour", "Ocean surface stress", "Sea surface height", "Subsurface temperature", "Surface currents", "Sea surface salinity", "Subsurface salinity", "Ocean surface heat flux", "Biotoxins / Phycotoxins", "Best Practice", "Manual"]
}
```

## About

The [`about`](https://schema.org/about) attribute allows for more detailed terminology to be assigned to keyword than the (keywords)[#keywords] attribute. 

```json
{
	"@context": {"@vocab": "https://schema.org/"},
	"@type": "CreativeWork",
	"keywords":
}
```

## Identifiers

## Example
Taking an example Best Practice from the repository, [_"Creating a weekly Harmful Algal Bloom bulletin. Version 1.0. [Best Practie Description Document]"_](https://repository.oceanbestpractices.org/handle/11329/424) a Schema.org representation, which would be embedded within the landing page for the repository is as follows:

```json
{
	"@context": "https://schema.org/",
	"@type": "CreativeWork",
	"@id": "https://repository.oceanbestpractices.org/handle/11329/424",
	"numberOfPages": 59,
	"author": [
		{"@type": "Person", "familyName": "Leadbetter", "givenName": "Adam"},
		{"@type": "Person", "familyName": "Silke", "givenName": "Joe"},
		{"@type": "Person", "familyName": "Cusack", "givenName": "Caroline"}
	],
	"maintainer": {"@type": "Person", "familyName": "Leadbetter", "givenName": "Adam", "email": "adam.leadbetter@marine.ie"},
	"keywords": ["Parameter Discipline::Biological oceanography::Macroalgae and seagrass", "Parameter Discipline::Biological oceanography::Phytoplankton", "Phytoplankton biomass and diversity", "Sea surface temperature", "Ocean colour", "Ocean surface stress", "Sea surface height", "Subsurface temperature", "Surface currents", "Sea surface salinity", "Subsurface salinity", "Ocean surface heat flux", "Biotoxins / Phycotoxins", "Best Practice", "Manual"]
}
```

## Version history

- **_1.0_** - 16th June 2020 - Initial draft 
