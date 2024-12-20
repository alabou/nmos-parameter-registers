# NMOS Source Attributes
{:.no_toc}

This Source Attributes parameter register contains extensible attributes and their permitted values which may be used in Source resources within the [AMWA IS-04 NMOS Discovery and Registration Specification](https://specs.amwa.tv/is-04).

- A markdown unordered list which will be replaced with the ToC, excluding the "Contents header" from above
{:toc}

## Criteria

- Each entry MUST be associated with an existing defined [NMOS Format](../formats).
- Each entry MUST define or refer to an existing unique attribute name within the scope of a Source.
- Each entry MUST have a short description.
- Each entry MUST identify any AMWA Specifications and versions from which it is valid.
- Each entry MUST define all permitted values for the attribute, either via an explicit list, well-defined references or both.
- Entries MAY be used to expand the set of permitted values associated with an existing extensible attribute.
- Each entry MUST link to a schema definition held within this repository (unless covered by a schema within the original specification).
- Additions and updates to this parameter register are to be submitted via a Pull Request (PR) according to the [General Procedures and Criteria](../common/).

As noted in [IS-04 v1.3](https://specs.amwa.tv/is-04/v1.3.2/docs/Behaviour_-_Nodes.html#all-resources), new Source attributes may be defined here as opposed to requiring a new version of the specification.

Query APIs and their clients which support v1.3 of IS-04 or operate in a mixed-version environment MUST be tolerant to the presence of Source attributes and values which may be added at a later date. This is further detailed in the [IS-04 Upgrade Path](https://specs.amwa.tv/is-04/v1.3.1/docs/6.0._Upgrade_Path.html) document.

## Attributes

Note: JSON schemas supporting validation of all the attributes will be defined in this register.
These MAY be used in addition to the schemas, such as _source_generic.json_ and _source_audio.json_, found in the AMWA IS-04 specification.

### receiver_id
- **Name:** `urn:x-matrox:receiver_id`
- **Description:** This attributes indicates the Receiver providing the essence to the Source.
- **Specification:** [AMWA IS-04](https://specs.amwa.tv/IS-04/v1.3)
- **Applicability:** 
- **Permitted Values:**
  - The UUID of a Receiver.

### layer
- **Name:** `urn:x-matrox:layer`
- **Description:** This attributes indicates the Receiver's sub-Stream providing the essence to the Source.
- **Specification:** [AMWA IS-04](https://specs.amwa.tv/IS-04/v1.3), [Matrox Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
- **Applicability:** 
- **Permitted Values:**
  - The layer value matching a sub-Stream Constraint Set of the Receiver's Capabilities.

### synchronous_media
- **Name:** `urn:x-matrox:synchronous_media`
- **Description:** This attributes indicates the media is synchronous (true) or asynchronous (false) to the source reference clock. An unspecified attribute shall be interpreted according to the operational environment. For an ST-2110 environment an unspecified attribute must be interpreted as synchronous media. For an IPMX environment an unspecified attribute must be interpreted as an asynchronous media. If this attribute is not specified for a Source then the SDP transport file a=mediaclk attribute should be used to know about the media being synchronous or asynchronous.
- **Specification:** [AMWA IS-04](https://specs.amwa.tv/IS-04/v1.3)
- **Applicability:** 
- **Permitted Values:** true, false