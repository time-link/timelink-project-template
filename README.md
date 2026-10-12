# Timelink project template

This repository is a template for a **single-user, single-project Timelink home**: a
project directory associating a set of source files in Kleio notation with a database.

The Timelink web app and the Kleio server serve this directory as `timelink-home` in
single-user, single-project mode. The `.timelink-project` marker file in the root
identifies the directory as a Timelink project directory.

## Usage

This repository is not meant to be used directly: it should be the basis of a new
repository created for each new project.

### Create a new repository on GitHub based on a template

This is the recommended procedure. It will create a repository with the recommended
structure, including documentation.

You need an account with [GitHub](https://github.com).

1. Go to the [timelink-project-template](https://github.com/time-link/timelink-project-template) repository on GitHub.
2. Press the green button "Use this template".
3. Choose a new name for your project repository.
4. Edit this README file to describe the sources in this repository and usage license.

Full instructions at [creating a repository from a template](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/creating-a-repository-from-a-template) in the GitHub documentation.

### Create a new project with the Timelink CLI

If you have the `timelink` Python package installed:

```
timelink create project my-project
```

This clones the template into a new `my-project` directory.

## Directory layout

```
├── database
│   ├── backups        backups of the project database
│   └── sqlite         SQLite database files
├── etc
│   └── doc            pointers to the ongoing documentation
├── extras             auxiliary project files: working documents, scripts,
│                      downloaded material and derived data
├── identifications    exports of the identification (record linking) process
├── inferences         inference rules used when processing the source files
├── mappings           mappings between Kleio groups and database tables
├── notebooks          Jupyter notebooks for working with the project data
├── sources            source files in Kleio notation (.cli, .kleio)
├── structures         structure files describing the internal structure of each
│                      type of source
└── .timelink-project  marker file: identifies this directory as a Timelink project
```

The core directories (`database`, `extras`, `inferences`, `notebooks`, `sources`,
`structures`) follow the single-project `timelink-home` layout. `etc`,
`identifications` and `mappings` are additional directories used by the Kleio
server and by the record-linking workflow.

See the [Timelink documentation](https://time-link.github.io/timelink-docs/) for details.

## What is Timelink?

Timelink, formerly known as MHK (Micro History with Kleio) is an information system designed for processing person related information collected from historical sources.

Timelink provides:

* a notation (kleio) for textual transcription of historical sources, capable of capturing complex information about people and their relations in any type of historical documents.
* a text processor that extracts information from the kleio transcriptions, infers personal attributes and relations from agent roles in historical events and generates data in formats suitable for database import.
* a database management system capable of processing time varying attributes and relations, assist in reconstructing biographies and networks from fragmentary information.

Timelink is open source MIT License software available at http://github.com/joaquimrcarvalho/timelink

## Source collections included in this repository

* **Describe this repository collections here**

## License

Timelink software is distributed under a MIT license that includes usage for commercial purposes.

Kleio transcriptions of historical sources are not distributed under the same license.

Each Kleio transcription file is copyright of the person or persons that produced the transcription.
