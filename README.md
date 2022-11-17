# Introduction

The Open Threat Modeling Format (OTM) defines a platform independent way to define the threat model of any system.

OTM allows both humans and computers to understand what are the components of a system, how are they distributed, the security risks that could be exposed to attackers and the mitigations that could be implemented to avoid those vulnerabilities.

OTM can be used to document your system and threat model, to keep you threat model aware of the changes that happens in the system and many other use cases.

# Complete example

For a complete example see [EXAMPLE.yaml](EXAMPLE.yaml).

# Versions

The Open Threat Model specification is versioned using [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html) (semver) and follows the semver specification.

```
Current schema version: 0.1.0
```

# Format

An OTM document is itself a JSON object, which may be represented either in JSON or YAML format.

All field names in the specification are **case sensitive**. This includes all fields that are used as keys in a map.

The specification follows the same approach to JSON formats as the OpenAPI specification. See https://swagger.io/specification/ for more information.

# Data Types

Primitive data types in the OTM are based on the types supported by the [JSON Schema Specification Wright Draft 00](https://datatracker.ietf.org/doc/html/draft-wright-json-schema-00#section-4.2). Note that `integer` as a type is also supported and is defined as a JSON number without a fraction or exponent part. `null` is not supported as a type (see `nullable` for an alternative solution).

The formats available to be used within an OTM files are:

| Type       | Comment                                                                                                   |
| ---------- | --------------------------------------------------------------------------------------------------------- |
| `integer`  | signed 32 bits                                                                                            |
| `long`     | signed 64 bits (a.k.a long)                                                                               |
| `float`    |                                                                                                           |
| `double`   |                                                                                                           |
| `string`   |                                                                                                           |
| `richText` | Rich text fields are noted as supporting CommonMark markdown formatting.                                  |
| `boolean`  |                                                                                                           |
| `date`     | As defined by full-date - [RFC3339](https://xml2rfc.tools.ietf.org/public/rfc/html/rfc3339.html#anchor14) |
| `datetime` | As defined by date-time - [RFC3339](https://xml2rfc.tools.ietf.org/public/rfc/html/rfc3339.html#anchor14) |

# Schema

## OTM object

| Field           | Type                                              | Description                                                                                                                                                                                | Examples            |
| --------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------- |
| otmVersion      | string                                            | **REQUIRED** This field states the OTM version used in the current file. It is an important field in order to ensure backwards compatibility.                                              | `otmVersion: 0.1.0` |
| project         | [Project object](#project-object)                 | **REQUIRED** The project node represents the entity within all the other elements are grouped. It's the unit of work.                                                                      |                     |
| representations | [Representations object](#representations-object) | Representations define different ways in which the project may be represented. Representation is an abstract concept and there might be several implementations.                           |                     |
| assets          | [Assets object](#assets-object)                   | Assets are the different kinds of sensible information that take part in our threat model.                                                                                                 |                     |
| components      | [Components object](#components-object)           | Components are the different pieces of software / hardware that make up our project.                                                                                                       |                     |
| dataflows       | [DataFlows object](#dataflows-object)             | Data flows are the elements that describe the movement of relevant information (assets) across our architecture.                                                                           |                     |
| trustZones      | [TrustZones object](#trustzones-object)           | Trust zones are the different areas within which components are located. They define how trustworthy an area is, based on how accessible it is: the more accessible, the less trustworthy. |                     |
| threats         | [Threats object](#threats-object)                 | Threats are the undesirable outcomes that can occur in our system and that we want to prevent.                                                                                             |                     |
| mitigations     | [Mitigations object](#mitigations-object)         | Mitigations are the actions that we can take (or controls that we can put in place) in order to prevent a threat from taking place.                                                        |                     |

## Project object

The project node represents the entity within all the other elements are grouped. Its the unit of work.

<table>
<tr>    
    <th>Field</th>
    <th>Type</th>
    <th>Description</th>
    <th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name of the project</td>
<td>

    name: Project name

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the project.</td>
<td>

    id: project-example-id

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description for the project.</td>
<td>

    description: This is the threat model for the app 'MuCustomApp123

</td>
</tr>

<tr></tr>
<tr>
<td>owner</td>
<td>string</td>
<td>Name of the project's owner. This is the person responsible for the project.</td>
<td>

    owner: John Doe

</td>
</tr>

<tr></tr>
<tr>
<td>ownerContact</td>
<td>string</td>
<td>Project's owner contact email. </td>
<td>

    ownerContact: email@email.com

</td>
</tr>

<tr></tr>
<tr>
<td>tags</td>
<td>array of strings</td>
<td>	
Array of labels to tag the project</td>
<td>

    tags:
        - microservice
        - spring

</td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>This is a free-form map of attributes that complete the information about the project.</td>
<td>

    attributes:
        filePath: “file.xml”
        cmdbId: MyApp123

</td>
</tr>

</table>
<br />

#### Example

```yaml
project:
  name: Test project
  id: test-project
  description: This is a test project for the OTM development
  owner: John Doe
  ownerContact: john.doe@example.com
  attributes:
    filePath: “file.xml”
    cmdbId: MyApp123
```

## Representations object

This node can define several ways on which the project can be represented.

Representation is an abstract concept and there might be several implementations.

These are the currently supported representation types:

- `diagram`
- `code`
- `threat-model`

Each representation has these fields:

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name for the representation.</td>
<td>

    name: Architecture diagram

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the representation.</td>
<td>

    id: architecture-diagram-id

</td>
</tr>

<tr></tr>
<tr>
<td>type</td>
<td>string</td>
<td><b>REQUIRED</b> Type of representation.</td>
<td>

    type: diagram

</td>
</tr>
<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description of the representation content and usage.</td>
<td>

    description: This is a diagram of the project's architecture

</td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>	
This is a free-form list of attributes that complete the description of the representation.</td>
<td>

    attributes:
        language: java
        platform: github
        vcs: git

</td>
</tr>

</table>
<br />

#### Example

```yaml
representations:
  - name: Architecture Diagram
    id: architecture-diagram
    description: This is a diagram of the project's architecture
    type: diagram
    size:
      width: 1000
      height: 1000
    attributes:
      platform: drawio
      unit: pixel
  - name: Application Code
    id: application-code
    type: code
    repository:
      url: https://github.com/my-project
    attributes:
      language: java
      platform: github
      vcs: git
```

## Representation supported types

Depending on the type selected, some extra fields must be included in the representation. The supported representation types are:

### Diagram

Represents a diagram with very basic information.

Under the type “diagram“ we have the following extra fields:

| Field | Type                        | Description                                                                  | Examples |
| ----- | --------------------------- | ---------------------------------------------------------------------------- | -------- |
| size  | [Size object](#size-object) | **REQUIRED** Object that contains the information regarding the diagram size |          |

#### Example

```yaml
representations:
  - name: Architecture Diagram
    id: architecture-diagram
    description: This is a diagram of the project's architecture
    type: diagram
    size:
      width: 1000
      height: 1000
    attributes:
      background-color: blue
      transparent: 40
```

### Code

Represents a repository of code.

Under the type “code“ we have the following extra fields:

| Field      | Type                                    | Description                                                                    | Examples |
| ---------- | --------------------------------------- | ------------------------------------------------------------------------------ | -------- |
| repository | [Repository object](#repository-object) | Contains information about the Repository where the referenced code is located |          |

#### Example

```yaml
representations:
  - name: Application Code
    id: application-code
    type: code
    repository:
      url: https://github.com/my-project
    attributes:
      language: java
      framework: spring
```

### Threat-Model

Represents a threat model.

Under the type “threat-model“ we have no extra fields.

#### Example

```yaml
representations:
  - name: Architecture Threat Model
    id: architecture-threat-model
    type: threat-model
    attributes:
      source: Microsoft Threat Model
      template: custom
```

## RepresentationElement object

The representation element stated how an element is represented with the available representations.

In the current version we support three types of representation types as was mentioned here [OTM version 0.1.0 | Representations-object](#representations-object):

- diagram
- code
- threat-model

Therefore, there can be also three types of representation instances:

### Representation element for diagram

Represents an element of a diagram.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>representation</td>
<td>string</td>
<td><b>REQUIRED</b> Id of the representation on which this element is represented</td>
<td>

    representation: architecture-diagram

</td>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td>Name for the representation element.</td>
<td>

    name: Component Box

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier of the current representation instance</td>
<td>

    id: component-box-id

</td>
</tr>

<tr></tr>
<tr>
<td>position</td>
<td><a href="#position-object">Position object</a></td>
<td><b>REQUIRED</b> This node contains all the information about the location of the element within the diagram.</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>size</td>
<td><a href="#size-object">Size object</a></td>
<td><b>REQUIRED</b> This node contains all the information regarding the size of the shape.</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map &lt;string, string&gt;</td>
<td>This is a free-form map of attributes that complete the description of the representation.</td>
<td>

    attributes:
      color: red
      shape: square

</td>
</tr>
</table>
<br/>

#### Example

```yaml
representations:
  representation: architecture-diagram
  name: Private Box
  id: private-box-shape
  position:
    x: 0
    y: 0
  size:
    with: 100
    height: 100
attributes:
  color: red
  shape: square
```

### Representation element for code

Despite all fields being optional, at least one of them is required.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>representation</td>
<td>string</td>
<td><b>REQUIRED</b> Id of the representation on which this element is represented</td>
<td>

    representation: code-repository

</td>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td>Name for the representation element.</td>
<td>

    name: Example Class

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier of the current representation instance</td>
<td>

    id: org.example.class

</td>
</tr>

<tr></tr>
<tr>
<td>file</td>
<td>string</td>
<td>File where the representative code is located</td>
<td>

    file: path/to/class.java

</td>
</tr>

<tr></tr>
<tr>
<td>line</td>
<td>integer</td>
<td>Number of the code line that represents the element</td>
<td>

    line: 324

</td>
</tr>

<tr></tr>
<tr>
<td>codeSnippet</td>
<td>richText</td>
<td>Code that represents the element</td>
<td>

    codeSnippet: |
      public void createOTM(String[] args) {
        Scanner reader = new Scanner(System.in);
        System.out.print("Enter a number: ");

        int number = reader.nextInt()
        System.out.println("You entered: " + number);
    }

</td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map &lt;string, string&gt;</td>
<td>This is a free-form list of attributes that complete the description of the representation.</td>
<td>

    attributes:
      source: sonar
      author: John Doe

</td>
</tr>

</table>
<br/>

#### Example

```yaml
representations:
  representation: code-repository
  id: org.example.class
  name: Example Class
  file: path/to/class.java
  line: 324
  codeSnippet: |
    public void createOTM(String[] args) {
      Scanner reader = new Scanner(System.in);
      System.out.print("Enter a number: ");
      
      int number = reader.nextInt()
      System.out.println("You entered: " + number);
    }
  attributes:
    source: sonar
    author: John Doe
```

### Representation element for threat-model

Represents an element of a threat model.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>representation</td>
<td>string</td>
<td><b>REQUIRED</b> Id of the representation on which this element is represented</td>
<td>

    representation: architecture-threat-model

</td>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td>Name for the representation element.</td>
<td>

    name: Threat model representation

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier of the current representation instance</td>
<td>

    id: threat-model-representation-id

</td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map &lt;string, string&gt;</td>
<td>This is a free-form list of attributes that complete the description of the representation.</td>
<td>

    attributes:
      author: John Doe

</td>
</tr>

</table>
<br/>

#### Example

```yaml
representations:
  representation: architecture-threat-model
  id: threat-model-representation-id
  name: Threat model representation
  attributes:
    author: John Doe
```

## Assets object

Assets are the different kinds of sensible information that take part in our threat model.

<table>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the asset</td>
<td>

    id: cc-data

</td>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name for the defined assets</td>
<td>

    name: Credit card data

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description for the asset</td>
<td>

    description: This is our customer’s credit card numbers

</td>
</tr>

<tr></tr>
<tr>
<td>risk</td>
<td><a href="#assetrisk-object">AssetRisk object</a></td>
<td><b>REQUIRED</b> AssetRisk influences impact with regard to a threat.</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>This is a free-form map of attributes that complete the description of the asset.</td>
<td>

    attributes:
      attr1: value1
      attr2: value2

</td>
</tr>

</table>
<br />

#### Example

```yaml
assets:
    - name: Credit Card Data
    id: cc-data
    description: Credit card numbers used for payments in the platform
    risk:
      confidentiality: 100
      integrity: 100
      availability: 100
      comment: We have decided that the values are a 100 for all values since this highly sensitive information
    attributes:
      attr1: value1
      attr2: value2
  - name: Public Info
    id: public-info
    description: Public information meant to be seen by any interested customer
    risk:
      confidentiality: 0
      integrity: 100
      availability: 50
      comment: Public information has no confidentiality at all but it is quite important for it to be available and to not be changed by attakers
    attributes:
```

## AssetRisk object

AssetRisk influences impact with regard to a threat.

Those values are passed through OTM into the IR rules engine which performs the calculation for inherent risk.

More information - [https://support.iriusrisk.com/hc/en-us/articles/4412644787345-How-is-inherent-risk-calculated-](https://support.iriusrisk.com/hc/en-us/articles/4412644787345-How-is-inherent-risk-calculated-)


<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>confidentiality</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 to 100. How bad would it be to have an attacker see this information?</td>
<td>

    confidentiality: 50

</td>
</tr>

<tr></tr>
<tr>
<td>integrity</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 to 100. How bad would it be to have an attacker modify this information?</td>
<td>

    integrity: 50

</td>
</tr>

<tr></tr>
<tr>
<td>availability</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 to a 100. How bad would it be to lose this information or have it inaccessible in our system?
</td>
<td>

    availability: 50

</td>
</tr>

<tr></tr>
<tr>
<td>comment</td>
<td>richText</td>
<td>Short explanation on why we have selected the different risk values</td>
<td>

    comment: We have decided that the values are a 100 for all values since this highly-sensitive information

</td>
</tr>

</table>

## Asset Instance object

Object that describes the relationship between the component and the different assets.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<!-- row -->
<tr></tr>
<tr>
<td>processed</td>
<td>array of strings</td>
<td>Array of ids that represent the assets that are processed in this component.</td>
<td>

    assets:
      processed:
        - asset1
        - asset2

</td>
</tr>

<tr></tr>
<tr>
<td>stored</td>
<td>array of strings</td>
<td>Array of ids that represent the assets that are stored within the described component.</td>
<td>

    assets:
      stored:
        - asset1
        - asset2

</td>
</tr>

</table>
<br />

#### Example

```yaml
assets:
  processed:
    - 441b01ca-2653-4707-8be8-fd6addce9df6
    - 4136bb34-e2ff-11eb-ba80-0242ac130004
  stored:
    - 441b01ca-2653-4707-8be8-fd6addce9df6
```

## Components object

Components are the different pieces of software / hardware that make our project. These are the fields for them:

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<!-- row -->
<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name for the defined component</td>
<td>

    name: Payments service

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the component</td>
<td>

    id: payment-service

</td>
</tr>

<tr></tr>
<tr>
<td>type</td>
<td>string</td>
<td><b>REQUIRED</b> The kind of the described component</td>
<td>

    type: ec2-instance

</td>
</tr>

<tr></tr>
<tr>
<td>tags</td>
<td>array of strings</td>
<td>List of tags related to the component.</td>
<td>

    tags:
      - web
      - server

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description for the components</td>
<td>

    description: This is the server in charge of processing the payments in the platform

</td>
</tr>

<tr></tr>
<tr>
<td>parent</td>
<td><a href="#parent-object">Parent object</a></td>
<td><b>REQUIRED</b> Element in which this component is currently enclosed. It can be either a trust zone or another 
component. It should contain an attribute name stating the component type to avoid ambiguity.
<br/>A component must have just <b>one parent</b>: another component or a trust zone.
</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>representations</td>
<td>array of <a href="#representations-object">Representation Element object</a></td>
<td>Array of the representations that this component has.</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>assets</td>
<td><a href="#asset-instance-object">Asset instance object</a></td>
<td>Object that describes the relationship between the component and the different assets</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>threats</td>
<td>array of <a href="#threat-instance-object">Threat instance object</a></td>
<td>Array of threats that are related to the current component.</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>This is a free-form map of attributes that complete the description of the component.</td>
<td>

    attributes:
      attr1: value1
      attr2: value2

</td>
</tr>

</table>

#### Example

```yaml
components:
  - name: Web Service
    id: web-service
    type: web-service
    description: Runs our web application
    parent:
      trustZone: private
    tags:
      - tomcat
    representations:
      - representation: architecture-diagram
        id: web-service-box
        name: Web Service
        position:
          x: 100
          y: 100
        size:
          width: 50
          height: 50
    assets:
      processed:
        - 441b01ca-2653-4707-8be8-fd6addce9df6
        - 4136bb34-e2ff-11eb-ba80-0242ac130004
      stored:
        - 441b01ca-2653-4707-8be8-fd6addce9df6
    threats:
      - threat: 22724267-be7e-44c0-8b1f-d7d33e9a34ec
        state: exposed
        mitigations:
          - mitigation: fd6136f4-e2ff-11eb-ba80-0242ac130004
            state: implemented
    attributes:
      - owner: John Doe
      - department: IT
  - name: Customer Database
    id: customer-database
    description: Postgres database
    parent:
      trustZone: private
    type: database
    tags:
      - postgres
    representations:
      - represetation: architecture-diagram
        id: box-for-postgress-DB
        position:
          x: 200
          y: 100
        size:
          width: 50
          height: 50
  - name: Class CustomerDatabase
    id: class-customerdatabase
    description: Managages customer database
    type: code-class
    parent:
      trustZone: private
    representations:
      - representation: application-code
        id: source-to-go-class
        name: source.go
        file: path/to/source.go
        line: 644
```

## TrustZones object

Trust zones are the different areas within which components are located. They define how trustworthy an area is, based on how accessible it is: the more accessible, the less trustworthy.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name for the defined trust zone</td>
<td>

    name: Internet

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the trust zone</td>
<td>

    id: internet

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description for the trust zone</td>
<td>

    description: >
      This is the world
      wide web accesible
      for every one with
      an internet
      connection

</td>
</tr>

<tr></tr>
<tr>
<td>risk</td>
<td><a href="#trustzonerisk-object">TrustZoneRisk object</a></td>
<td><b>REQUIRED</b> This is the object that describes the different aspects of risk associated with the trust zone</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>parent</td>
<td><a href="#parent-object">Parent object</a></td>
<td>	
Unique identifier of the component or trust zone enclosing this trust zone. It should contain an attribute name stating the element type.<br />
A trust zone can have <b>zero or one parent</b>: another component or a trust zone.
</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>representations</td>
<td>array of <a href="#representationelement-object">Representation Element object</a></td>
<td>Array of the representations that this trust zone has</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>This is a free-form map of attributes that complete the description of the trust zone.</td>
<td>

    attributes:
      attr1: value1
      attr2: value2

</td>
</tr>

</table>
<br />

#### Example

```yaml
trustzones:
  - name: Internet
    id: internet
    description: This is the internet trust zone
    risk:
      trustRating: 20
    representations:
      representation: architecture-diagram
      id: internet-box-shape
      name: Internet
      position:
        x: 600
        y: 100
      size:
        width: 100
        height: 100
    attributes:
      attr1: value1
      attr2: value2
  - name: Private
    id: private
    description: Private trustzone for protected components
    risk:
      trustRating: 15
    parent: internet
    representations:
      representation: architecture-diagram
      id: private-box-shape
      name: Private
      postion:
        x: 0
        y: 0
      size:
        with: 100
        height: 100
    attributes:
```

## TrustZoneRisk object

This is the object that describes the different aspects of risk associated with the trust zone.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>trustRating</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 and 100. How trustworthy is this trust zone?</td>
<td>

    trustRating: 10

</td>
</tr>
</table>

#### Example

```yaml
risk:
  trustRating: 20
```

## Parent object

Element that encloses another element. It can be either a trust zone or a component. Currently, we have two supported types of parents:

- trustZone
- component

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>trustZone</td>
<td>string</td>
<td>	
Id of the element in which this component is currently enclosed. It can be either a trust zone or another component. It should contain an attribute name stating the component type to avoid ambiguity</td>
<td>

    trustZone: private

</td>
</tr>

<tr></tr>
<tr>
<td>component</td>
<td>string</td>
<td>Id of the element in which this component is currently enclosed. It can be either a trust zone or another component. It should contain an attribute name stating the component type to avoid ambiguity</td>
<td>

    component: web-server

</td>
</tr>
</table>
<br />

#### Example

```yaml
parent:
  trustZone: private
```

```yaml
parent:
  component: web-server
```

## Dataflows object

Data flows are the elements that describe the movement of relevant information (assets) across our architecture.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name for the defined dataflow.</td>
<td>

    name: Credit card reporting

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the dataflow.</td>
<td>

    id: credit-card-reporting

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description of the dataflow content and usage.</td>
<td>

    description: Credit card information being exchanged in between the web app and the database

</td>
</tr>

<tr></tr>
<tr>
<td>tags</td>
<td>array of strings</td>
<td>Array of tags related to the dataflow.</td>
<td>

    tags:
      - http
      - https

</td>
</tr>

<tr></tr>
<tr>
<td>bidirectional</td>
<td>boolean</td>
<td>States if the information flows both ways.

By default, it is false.</td>

<td>

    bidirectional: true

</td>
</tr>

<tr></tr>
<tr>
<td>source</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the source component of the dataflow.</td>
<td>

    source: web-service

</td>
</tr>

<tr></tr>
<tr>
<td>destination</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the destination component of the dataflow.</td>
<td>

    destination: psotgress-db

</td>
</tr>

<tr></tr>
<tr>
<td>assets</td>
<td>array of strings</td>
<td>Array of assets that are transported by the dataflow.</td>
<td>

    assets:
      - cc-data
      - public-info

</td>
</tr>

<tr></tr>
<tr>
<td>threats</td>
<td>array of <a href="#threat-instance-object">Threat instance object</a></td>
<td>Array of threats that are related to the current dataflow.</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>This is a free-form map of attributes that complete the description of the dataflow.</td>
<td>

    attributes:
      attr1: value1
      attr2: value2

</td>
</tr>
</table>
<br />

#### Example

```yaml
dataflows:
  - name: Dataflow between webservice and mongo.
    id: cc-store-in-db
    description: Creditcard information being exchanged in between the web app and the data base
    bidirectional: true
    source: web-service
    target: customer-database
    tags:
      - http
      - https
    assets:
      - cc-data
    threats:
      - threat: 22724267-be7e-44c0-8b1f-d7d33e9a34ec
        state: exposed
        mitigations:
          - mitigation: fd6136f4-e2ff-11eb-ba80-0242ac130004
            state: required
    attributes:
      attr1: value1
      attr2: value2
```

## Threats object

Threats are the undesirable outcomes that can occur in our system and that we want to prevent. These are its fields:

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> This is the name for the threat</td>
<td>

    name: Attackers gain unauthorized access to the control of the environment

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the threat</td>
<td>

    id: LOSS-CONTROL_ENV

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short description of the threat</td>
<td>

    description: Attackers could potentially gain unauthorized access to the control of the environment, due to user accounts - or role groups - not being well-defined and configured. As a consequence, attackers may be able to make changes without root approval.

</td>
</tr>

<tr></tr>
<tr>
<td>categories</td>
<td>array of strings</td>
<td>Array of categories that are applicable to the threat</td>
<td>

    categories:
      - Spoofing
      - Authentication

</td>
</tr>

<tr></tr>
<tr>
<td>cwes</td>
<td>array of strings</td>
<td>Array of CWE identifiers of weaknesses associated with the threat</td>
<td>

    cwes:
      - CWE-79
      - CWE-787

</td>
</tr>

<tr></tr>
<tr>
<td>risk</td>
<td><a href="#threatrisk-object">ThreatRisk object</a></td>
<td><b>REQUIRED</b> This object describes different aspects of risk (likelihood and impact) posed by the threat</td>
<td></td>
</tr>

<tr></tr>
<tr>
<td>tags</td>
<td>array of strings</td>
<td>Array of tags related to the threat</td>
<td>

    tags:
      - unauthorized-access
      - loss-control

</td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>Map [string, string]</td>
<td>This is a free-form map of attributes that complete the description of the threat.</td>
<td>

    attributes:
      expirationDate: “2021-05-17”
      cmdbId: MyApp123

</td>
</tr>

</table>
<br />

#### Example

```yaml
threats:
  - name: Attackers gain unauthorized access to the control of the environment
    id: LOSS-CONTROL_ENV
    description: Attackers could potentially gain unauthorized access to the control of the environment, due to user accounts - or role groups - not being well defined and configured. As a consequence, attackers may be able to make changes without root approval.
    categories:
      - Spoofing
      - Tampering
    cwes:
      - CWE-79
      - CWE-787
    risk:
      likelihood: 50
      likelihoodComment: It is reasonable to think this might happen but it requires for the attaketr to have a deep cyprografy knowledge
      impact: 100
      impactComment: If this threat becomes a rallity company will strruggle to keep customers and the monetory loss would jeopardise the whole company
    attributes:
      expirationDate: 2021-05-17
      cmdbId: MyApp123
    tags:
      - loss-control
      - environment
```

## ThreatRisk object

Risk information for the associated threat.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>likelihood</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 to 100. How likely is it that this threat will take place?</td>
<td>

    likelihood: 50

</td>
</tr>

<tr></tr>
<tr>
<td>likelihoodComment</td>
<td>richText</td>
<td>Short explanation of why we have selected such a value for the likelihood</td>
<td>

    likelihoodComment: It is reasonable to think that this might happen, but it requires that the attacker has a deep knowledge of cryptography

</td>
</tr>

<tr></tr>
<tr>
<td>impact</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 to 100. How bad would it be if this threat took place?</td>
<td>

    impact: 100

</td>
</tr>

<tr></tr>
<tr>
<td>impactComment</td>
<td>richText</td>
<td>Short explanation of why we have selected such a value for the impact</td>
<td>

    impactComment: If this threat becomes a reality, the company will struggle to keep customers and the monetary loss would jeopardize the business

</td>
</tr>

</table>
<br/>

#### Example

```yaml
risk:
  likelihood: 50
  likelihoodComment: It is reasonable to think that this might happen, but it requires that the attacker has a deep knowledge of cryptography
  impact: 100
  impactComment: If this threat becomes a reality, the company will struggle to keep customers and the monetary loss would jeopardize the business
```

## Threat instance object

This object stores a reference to a threat and add additional data enclosed in a particular scope.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>threat</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier of the related threat. It should be one of the threats described in the root node 
threats.</td>
<td>

     threat: 22724267-be7e-44c0-8b1f-d7d33e9a34ec

</td>
</tr>

<tr></tr>
<tr>
<td>state</td>
<td>string</td>
<td><b>REQUIRED</b> Describes the state in which the threat currently is.</td>
<td>

    state: mitigated

</td>
</tr>

<tr></tr>
<tr>
<td>mitigations</td>
<td>array of <a href="#mitigation-instance-object">Mitigation instance object</a></td>
<td>Array of mitigation that can prevent the threat from taking place.</td>
<td></td>
</tr>
</table>

#### Example

```yaml
threats:
  - threat: 22724267-be7e-44c0-8b1f-d7d33e9a34ec
    state: exposed
    mitigations:
      - mitigation: fd6136f4-e2ff-11eb-ba80-0242ac130004
        state: implemented
```

## Mitigations object

Mitigations are the actions that we can take (or controls that we can put in place) in order to prevent a threat from taking place.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>name</td>
<td>string</td>
<td><b>REQUIRED</b> Name for the mitigation</td>
<td>

    name: Use strong passwords

</td>
</tr>

<tr></tr>
<tr>
<td>id</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier for the mitigation</td>
<td>

    id: use-strong-passwords

</td>
</tr>

<tr></tr>
<tr>
<td>description</td>
<td>richText</td>
<td>Short descriptions of how to implement the mitigation</td>
<td>

    description: Force users to use passwords over 10 characters, containing letters numbers and symbols

</td>
</tr>

<tr></tr>
<tr>
<td>riskReduction</td>
<td>integer</td>
<td><b>REQUIRED</b> From 0 to 100. How much will the threat risk decrease once this mitigation is implemented?</td>
<td>

    riskReduction: 75

</td>
</tr>

<tr></tr>
<tr>
<td>attributes</td>
<td>	
Map [string, string]</td>
<td>	
This is a free-form list of attributes that complete the description of the threat.</td>
<td>

    attributes:
      standard: OWASP-ASVS
      cmdbId: MyApp123

</td>
</tr>

</table>
<br />

#### Example

```yaml
mitigations:
  - name: This is the name of mitigation 1
    id: fd6136f4-e2ff-11eb-ba80-0242ac130004
    description: Description for mitigation 1
    riskReduction: 50
    attributes:
       standard: OWASP-ASVS
       cmdbId: MyApp123

  - name: Mitigation 2
    id: 3b837730-e300-11eb-ba80-0242ac130004
    description: Description for mitigation 2
    riskReduction 100
```

## Mitigation instance object

Mitigation that can prevent the threat from taking place.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>mitigation</td>
<td>string</td>
<td><b>REQUIRED</b> Unique identifier of the related mitigation. It should be declared in the root node mitigation.</td>
<td>

    mitigation: fd6136f4-e2ff-11eb-ba80-0242ac130004

</td>
</tr>

<tr></tr>
<tr>
<td>state</td>
<td>string</td>
<td><b>REQUIRED</b> State of the mitigation</td>
<td>

    state: implemented

</td>
</tr>

</table>
<br />

#### Example

```yaml
mitigations:
  - mitigation: fd6136f4-e2ff-11eb-ba80-0242ac130004
    state: implemented
```

## Repository object

Contains information about the Repository where the referenced code is located.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>url</td>
<td>string</td>
<td>Connection URL of the described repository</td>
<td>

    https://github.com/my-project

</td>
</tr>
</table>
<br />

#### Example

```yaml
repository:
  url: https://github.com/my-project
```

## Size object

Represents a very basic information about a size of an element.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>width</td>
<td>integer</td>
<td><b>REQUIRED</b> Width in pixels</td>
<td>

    width: 400

</td>
</tr>

<tr></tr>
<tr>
<td>height</td>
<td>integer</td>
<td><b>REQUIRED</b> Height in pixels</td>
<td>

    height: 300

</td>
</tr>
</table>

### Position object

Represents very basic information about the position of an element.

<table>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Examples</th>
</tr>

<tr></tr>
<tr>
<td>x</td>
<td>integer</td>
<td><b>REQUIRED</b> This is the position of the element in the X-axis in units</td>
<td>

    x: 200

</td>
</tr>

<tr></tr>
<tr>
<td>y</td>
<td>integer</td>
<td><b>REQUIRED</b> This is the position of the element in the Y-axis in units</td>
<td>

    y: 100

</td>
</tr>
</table>
<br />

#### Example

```yaml
position:
  x: 0
  y: 0
```

<p align="center">
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>
</p>
