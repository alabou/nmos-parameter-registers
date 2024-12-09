# NMOS Capabilities
{:.no_toc}

This Capabilities parameter register contains values that may be used to identify a capability, used in the `caps` property of the resources defined in the [AMWA IS-04 NMOS Discovery and Registration Specification](https://specs.amwa.tv/is-04).

- A markdown unordered list which will be replaced with the ToC, excluding the "Contents header" from above
{:toc}

## Criteria

- Capabilities used in the IS-04 `caps` properties are strongly RECOMMENDED to be included in this parameter register.
- Each entry MUST define a unique capability name (which is a string, with words separated by underscores, or a URN).
- Each entry MUST have a short description.
- Each entry MUST identify any AMWA Specifications and versions from which it is valid.
- Additions and updates to this parameter register are to be submitted via a Pull Request (PR) according to the [General Procedures and Criteria](../common/).

Query API clients MUST be tolerant to the presence of capabilities not yet defined here which may be added in later API versions.

Manufacturers MAY use their own namespaces to indicate capabilities which are not currently defined within the NMOS namespace (`urn:x-nmos:cap:`). In order to avoid collisions with simple names allocated by AMWA specifications, they MUST NOT use capability names that do not start with `urn:`.

Note: AMWA IS-04 specifies general requirements for the construction and [use of URNs](https://specs.amwa.tv/is-04/releases/v1.3.1/docs/2.1._APIs_-_Common_Keys.html#use-of-urns) in NMOS specifications.

Capabilities are most used by IS-04 Receivers to indicate what they may consume, but may be used by other `caps` objects in the future, potentially to indicate what they may be re-configured to generate.

## Values

### Media Types
- **Name:** `media_types`
- **Description:** Identifies Flows which may be created or consumed based upon their `media_type` attribute.
- **Specification:** [AMWA IS-04 v1.1](https://specs.amwa.tv/is-04/v1.1)
- **Applicability:** AMWA IS-04 since v1.1

### Event Types
- **Name:** `event_types`
- **Description:** Identifies Sources or Flows which may be created or consumed based upon their `event_type` attribute.
- **Specification:** [AMWA IS-04 v1.3](https://specs.amwa.tv/is-04/v1.3)
- **Applicability:** AMWA IS-04 since v1.3

### Constraint Sets
- **Name:** `constraint_sets`
- **Description:** Identifies streams from Senders which may be created or consumed based upon the attributes of the associated Source or Flow or contents of the associated transport file.
- **Specification:** [AMWA BCP-004-01](https://specs.amwa.tv/bcp-004-01/v1.0)
- **Applicability:** AMWA IS-04

### Version
- **Name:** `version`
- **Description:** String formatted TAI timestamp (`<seconds>:<nanoseconds>`) indicating when an attribute of the `caps` object last changed.
- **Specification:** [AMWA BCP-004-01](https://specs.amwa.tv/bcp-004-01/v1.0)
- **Applicability:** AMWA IS-04

## Constraint Set

Note: A JSON schema for a Constraint Set, supporting validation of all the Constraint Set Metadata and Parameter Constraints defined in this register, is available as **[constraint_set.json](constraint_set.json)**.
It MAY be used in place of the file with the same name in the AMWA BCP-004-01 specification.

## Constraint Set Metadata

### Label
- **Name:** `urn:x-nmos:cap:meta:label`
- **Description:** Freeform string label to provide a human-readable name for a Constraint Set.
- **Specification:** [AMWA BCP-004-01](https://specs.amwa.tv/bcp-004-01/v1.0)
- **Applicability:** AMWA IS-04

### Preference
- **Name:** `urn:x-nmos:cap:meta:preference`
- **Description:** Expresses the relative 'weight' that the Receiver assigns to its preference for the streams satisfied by the associated Constraint Set.
- **Specification:** [AMWA BCP-004-01](https://specs.amwa.tv/bcp-004-01/v1.0)
- **Applicability:** AMWA IS-04

### Enabled
- **Name:** `urn:x-nmos:cap:meta:enabled`
- **Description:** Indicates whether a Constraint Set is available to use immediately (true) or whether this is an offline capability which can be activated via some unspecified configuration mechanism (false).
- **Specification:** [AMWA BCP-004-01](https://specs.amwa.tv/bcp-004-01/v1.0)
- **Applicability:** AMWA IS-04

### Format
- **Name:** `urn:x-matrox:cap:meta:format`
- **Description:** Indicates the format associated with the Constraint Set
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** string
- **Applicability:** AMWA IS-04 v1.3

### Layer
- **Name:** `urn:x-matrox:cap:meta:layer`
- **Description:** Indicates the layer associated with the Constraint Set
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** integer
- **Applicability:** AMWA IS-04 v1.3

### Layer Compatibility Groups
- **Name:** `urn:x-matrox:cap:meta:layer_compatibility_groups`
- **Description:** Indicates the layer compatibility groups associated with the Constraint Set. A Constraint Set without a `urn:x-matrox:cap:meta:layer_compatibility_groups` attribute is assumed as being part of all groups.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** array of integer
- **Applicability:** AMWA IS-04 v1.3

## Parameter Constraints

### Media Type
- **Name:** `urn:x-nmos:cap:format:media_type`
- **Description:** Identifies streams which may be created or consumed based upon their IANA media type.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string
  - **Target:** (a) Flow `media_type` attribute, (b) SDP media description `m=` `<media>` and associated attribute `a=rtpmap:` `<encoding name>`
- **Applicability:** AMWA IS-04

### Grain Rate
- **Name:** `urn:x-nmos:cap:format:grain_rate`
- **Description:** Identifies streams which may be created or consumed based upon their grain rate.
- **Specification:** per AMWA BCP-004-01
  - **Type:** rational
  - **Target:** (a) Flow `grain_rate` (or from Source if omitted), (b) SDP attribute `a=fmtp:` format-specific parameter `exactframerate`
- **Applicability:** AMWA IS-04

### Frame Width
- **Name:** `urn:x-nmos:cap:format:frame_width`
- **Description:** Identifies the acceptable width in pixels of the picture in a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** (a) video Flow `frame_width`, (b) SDP attribute `a=fmtp:` format-specific parameter `width`
- **Applicability:** AMWA IS-04

### Frame Height
- **Name:** `urn:x-nmos:cap:format:frame_height`
- **Description:** Identifies the acceptable height in pixels of the picture in a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** (a) video Flow `frame_height`, (b) SDP attribute `a=fmtp:` format-specific parameter `height`
- **Applicability:** AMWA IS-04

### Interlace Mode
- **Name:** `urn:x-nmos:cap:format:interlace_mode`
- **Description:** Identifies the acceptable interlace mode of a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (enumerated values as per AMWA IS-04)
  - **Target:** (a) video Flow `interlace_mode`, (b) SDP attribute `a=fmtp:` format-specific parameters `interlace` and `segmented`
- **Applicability:** AMWA IS-04

### Colorspace
- **Name:** `urn:x-nmos:cap:format:colorspace`
- **Description:** Identifies the acceptable colorspace of a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (enumerated values as per AMWA IS-04 and the [Flow Attributes](../flow-attributes/#colorspace) register)
  - **Target:** (a) video Flow `colorspace`, (b) SDP attribute `a=fmtp:` format-specific parameter `colorimetry`
- **Applicability:** AMWA IS-04

### Transfer Characteristic
- **Name:** `urn:x-nmos:cap:format:transfer_characteristic`
- **Description:** Identifies the acceptable transfer characteristic system of a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (enumerated values as per AMWA IS-04 and the [Flow Attributes](../flow-attributes/#transfer-characteristic) register)
  - **Target:** (a) video Flow `transfer_characteristic`, (b) SDP attribute `a=fmtp:` format-specific parameter `TCS`
- **Applicability:** AMWA IS-04

### Color Sampling
- **Name:** `urn:x-nmos:cap:format:color_sampling`
- **Description:** Identifies the acceptable color (sub-)sampling mode of a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (enumerated values as per ST 2110-20 and the IANA [Media Type Sub-Parameter Registry for video/raw: Color (sub-)sampling][color-sampling])
  - **Target:** (a) SDP attribute `a=fmtp:` format-specific parameter `sampling`, (b) video Flow `components`
- **Applicability:** AMWA IS-04

### Component Depth
- **Name:** `urn:x-nmos:cap:format:component_depth`
- **Description:** Identifies the acceptable number of bits per component sample of a video stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** (a) SDP attribute `a=fmtp:` format-specific parameter `depth`, (b) video Flow `components.bit_depth`
- **Applicability:** AMWA IS-04

### Format Bit Rate
- **Name:** `urn:x-nmos:cap:format:bit_rate`
- **Description:** Identifies the acceptable bit rate of a compressed video or audio stream, in kilobits/second.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** coded video or audio Flow `bit_rate` (defined in the [Flow Attributes](../flow-attributes/#bit-rate) register)
- **Applicability:** AMWA IS-04

### Profile
- **Name:** `urn:x-nmos:cap:format:profile`
- **Description:** Identifies the acceptable profiles, as defined for the specific media type.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (values depending on the media type)
  - **Target:** (a) video Flow `profile` (defined in the [Flow Attributes](../flow-attributes/#profile) register), (b) depending on the media type, an SDP attribute `a=fmtp:` format-specific parameter, e.g. `profile`
- **Applicability:** AMWA IS-04

### Level
- **Name:** `urn:x-nmos:cap:format:level`
- **Description:** Identifies the acceptable levels, as defined for the specific media type.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (values depending on the media type)
  - **Target:** (a) video Flow `level` (defined in the [Flow Attributes](../flow-attributes/#level) register), (b) depending on the media type, an SDP attribute `a=fmtp:` format-specific parameter, e.g. `level`
- **Applicability:** AMWA IS-04

### Sublevel
- **Name:** `urn:x-nmos:cap:format:sublevel`
- **Description:** Identifies the acceptable sublevels, as defined for the specific media type.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (values depending on the media type)
  - **Target:** (a) coded video Flow `sublevel` (defined in the [Flow Attributes](../flow-attributes/#sublevel) register), (b) depending on the media type, an SDP attribute `a=fmtp:` format-specific parameter, e.g. `sublevel`
- **Applicability:** AMWA IS-04

### Channel Count
- **Name:** `urn:x-nmos:cap:format:channel_count`
- **Description:** Identifies the acceptable number of channels of an audio stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** (a) audio Source `channels`, (b) SDP attribute `a=rtpmap:` `<encoding parameters>`
- **Applicability:** AMWA IS-04

### Sample Rate
- **Name:** `urn:x-nmos:cap:format:sample_rate`
- **Description:** Identifies the acceptable number of samples per second in an audio stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** rational
  - **Target:** (a) audio Flow `sample_rate`, (b) SDP attribute `a=rtpmap:` `<clock rate>`
- **Applicability:** AMWA IS-04

### Sample Depth
- **Name:** `urn:x-nmos:cap:format:sample_depth`
- **Description:** Identifies the acceptable number of bits per sample of an audio stream.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** raw audio Flow `bit_depth`
- **Applicability:** AMWA IS-04

### Event Type
- **Name:** `urn:x-nmos:cap:format:event_type`
- **Description:** Identifies acceptable data streams based upon their event type.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (values as per AMWA IS-07 [Event types capability management](https://specs.amwa.tv/is-07/releases/v1.0.1/docs/3.0._Event_types.html#event-types-capability-management))
  - **Target:** data Flow `event_type`
- **Applicability:** AMWA IS-04

### Transport Bit Rate
- **Name:** `urn:x-nmos:cap:transport:bit_rate`
- **Description:** Identifies the acceptable bit rate of a network stream, in kilobits/second, including the transport overhead.
- **Specification:** per AMWA BCP-004-01
  - **Type:** integer
  - **Target:** (a) Sender `bit_rate` (defined in the [Sender Attributes](../sender-attributes/#bit-rate) register), (b) depending on the media type, SDP application-specific bandwidth `b=AS:`, for example as per ST 2110-22
- **Applicability:** AMWA IS-04

### Packet Time
- **Name:** `urn:x-nmos:cap:transport:packet_time`
- **Description:** Identifies the acceptable length of time in milliseconds represented by the media in a packet.
- **Specification:** per AMWA BCP-004-01
  - **Type:** number (as per [RFC 4566][RFC-4566])
  - **Target:** SDP attribute `a=ptime:` `<packet time>`
- **Applicability:** AMWA IS-04

### Max Packet Time
- **Name:** `urn:x-nmos:cap:transport:max_packet_time`
- **Description:** Identifies the acceptable maximum amount of media that can be encapsulated in each packet, expressed as time in milliseconds.
- **Specification:** per AMWA BCP-004-01
  - **Type:** number (as per [RFC 4566][RFC-4566])
  - **Target:** SDP attribute `a=maxptime:` `<maximum packet time>`
- **Applicability:** AMWA IS-04

### Packet Transmission Mode
- **Name:** `urn:x-nmos:cap:transport:packet_transmission_mode`
- **Description:** Identifies the acceptable JPEG XS packetization and transmission mode.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (enumerated values as per the [Sender Attributes](../sender-attributes/#packet-transmission-mode) register)
  - **Target:** (a) Sender `packet_transmission_mode` (defined in the Sender Attributes register), (b) SDP attribute `a=fmtp:` format-specific parameters `packetmode` and `transmode`, per [RFC 9134][RFC-9134]
- **Applicability:** AMWA IS-04

### ST 2110-21 Sender Type
- **Name:** `urn:x-nmos:cap:transport:st2110_21_sender_type`
- **Description:** Identifies the ST 2110-21 receiver capabilities, expressed as the acceptable sender type or types.
- **Specification:** per AMWA BCP-004-01
  - **Type:** string (enumerated values as per ST 2110-21, such as `2110TPNL` for narrow linear senders)
  - **Target:** (a) Sender `st2110_21_sender_type` (defined in the [Sender Attributes](../sender-attributes/#st-2110-21-sender-type) register), (b) SDP attribute `a=fmtp:` format-specific parameter `TP`
- **Applicability:** AMWA IS-04

### Constant Bit Rate
- **Name:** `urn:x-matrox:cap:format:constant_bit_rate`
- **Description:** Identifies the `bit_rate` of a Flow as being constant or variable.
- **Specification:** [Matrox Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Matrox Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
- **Type:** boolean
- **Target:** (a) Flow's `constant_bit_rate` attribute
- **Applicability:** AMWA IS-04 v1.3

### Audio Layers
- **Name:** `urn:x-matrox:cap:format:audio_layers`
- **Description:** Provide a minimum, maximum or list of layers allowed for multiplexed stream.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md), [Flow Attributes](https://github.com/alabou/NMOS-MatroxOnly/blob/main/FlowAttributes.md)
  - **Type:** integer
  - **Target:** (a) Flow `urn:x-matrox:audio_layers` attribute of a mux Flow, (b) Number of audio sub-streams of a mux Receiver.
- **Applicability:** AMWA IS-04 v1.3

### Video Layers
- **Name:** `urn:x-matrox:cap:format:video_layers`
- **Description:** Provide a minimum, maximum or list of layers allowed for multiplexed stream.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md), [Flow Attributes](https://github.com/alabou/NMOS-MatroxOnly/blob/main/FlowAttributes.md)
  - **Type:** integer
  - **Target:** (a) Flow `urn:x-matrox:video_layers` attribute of a mux Flow, (b) Number of video sub-streams of a mux Receiver.
- **Applicability:** AMWA IS-04 v1.3

### Data Layers
- **Name:** `urn:x-matrox:cap:format:data_layers`
- **Description:** Provide a minimum, maximum or list of layers allowed for multiplexed stream.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md), [Flow Attributes](https://github.com/alabou/NMOS-MatroxOnly/blob/main/FlowAttributes.md)
  - **Type:** integer
  - **Target:** (a) Flow `urn:x-matrox:data_layers` attribute of a mux Flow, (b) Number of data sub-streams of a mux Receiver.
- **Applicability:** AMWA IS-04 v1.3

### HKEP
- **Name:** `urn:x-matrox:cap:transport:hkep`
- **Description:** Indicate that the Receiver / Sender supports HDCP / HKEP protected streams. A value false means that HDCP / HKEP streams are not supported, a value true means that only HDCP / HKEP streams are supported, a value { true, false } or {} indicate that both HDCP / HKEP protected streams and non-protected streams are supported.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md), [HKEP](https://vsf.tv/download/technical_recommendations/VSF_TR-10-5_2022-03-22.pdf)
  - **Type:** boolean
  - **Target:** (a) SDP attribute `a=hkep:` parameter 
- **Applicability:** AMWA IS-04 v1.3

### Privacy
- **Name:** `urn:x-matrox:cap:transport:privacy`
- **Description:** Indicate that the Receiver / Sender supports Privacy Encryption Protocol (PEP) protected streams. A value false means that PEP streams are not supported, a value true means that only PEP streams are supported, a value { true, false } or {} indicate that both PEP protected streams and non-protected streams are supported.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md), [PEP](https://vsf.tv/download/technical_recommendations/VSF_TR-10-13_2024-02-13.pdf)
  - **Type:** boolean
  - **Target:** (a) SDP attribute `a=privacy:` parameter (b) IS-05 `ext_privacy` transport parameters
- **Applicability:** AMWA IS-04 v1.3

### Channel Order
- **Name:** `urn:x-matrox:cap:transport:channel_order`
- **Description:** Provides the ordering of channels into groups as per ST 2110-30 and ST 2110-31 channel grouping symbols for PCM streams and opaque AM824 streams. This capability should not be used for fully described AM824 streams as the sub-streams capabilities are much more expressive. The SMPTE2110 channel-order convention is used as in the following example "SMPTE2110.(51,ST)" having two groups for a total of 8 channels.
- **Specification:** SMPTE ST 2110-30 and ST 2110-31, [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md), [NMOS With AES3](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20AES3.md)
  - **Type:** string
  - **Target:** (a) SDP channel-order parameter of PCM streams and opaque AM824 streams.
- **Applicability:** AMWA IS-04 v1.3

### Parameter Sets Transport Mode
- **Name:** `urn:x-matrox:cap:transport:parameter_sets_transport_mode`
- **Description:** Identifies the acceptable parameter sets transport modes.
- **Specification:** [Matrox Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Matrox Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** string (enumerated values as per the specifications [H.264](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20H.264.md), [H.265](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20H.265.md), [AAC](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20AAC.md))
  - **Target:** (a) Sender `parameter_sets_transport_mode`, (b) SDP attribute `a=fmtp:` format-specific parameter `sprop-parameter-sets`, per [RFC 6184][RFC-6184], (c) SDP attribute `a=fmtp:` format-specific parameters `sprop-vps`, `sprop-sps` and `sprop-pps`, per [RFC 7798][RFC-7798], (d) SDP attribute `a=fmtp:` format-specific parameter `config` per [RFC 6416][RFC-6416]
- **Applicability:** AMWA IS-04 v1.3

### Parameter Sets Flow_mode
- **Name:** `urn:x-matrox:cap:transport:parameter_sets_flow_mode`
- **Description:** Identifies the acceptable parameter sets flow modes.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** string (enumerated values as per the specifications [H.264](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20H.264.md), [H.265](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20H.265.md), [AAC](https://github.com/alabou/NMOS-MatroxOnly/blob/main/NMOS%20With%20AAC.md))
  - **Target:** (a) Sender `parameter_sets_flow_mode`
- **Applicability:** AMWA IS-04 v1.3

### Clock Ref Type
- **Name:** `urn:x-matrox:cap:transport:clock_ref_type`
- **Description:** Identifies the acceptable clock reference supported by a Receiver. The clock associated with a Flow is identified by the `clock_name` attribute of the Source associated with the Flow. The value `internal` implies recovering the Sender's internal clock, while the value `ptp` implies using the common reference clock. 
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** string (enumerated values as per IS-04 schema clock_internal.json `internal` and clock_ptp.json `ptp`)
  - **Target:** (a) `ref_type` of Source's associated `clock_name` clock. (b) SDP a=ts-refclk attributes
- **Applicability:** AMWA IS-04 v1.3

### Synchronous Media
- **Name:** `urn:x-matrox:cap:transport:synchronous_media`
- **Description:** Identifies the acceptable media types supported by a Receiver. A media is either synchronous or asynchronous to the reference clock. A receiver may support either or both types.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** boolean
  - **Target:** (a) `urn:x-matrox:synchronous_media` attribute of a Source. (b) SDP a=mediaclk attribute (`sender` implies asynchronous, `direct` implies synchronous)
- **Applicability:** AMWA IS-04 v1.3

### Info Block
- **Name:** `urn:x-matrox:cap:transport:info_block`
- **Description:** Identifies if the Receiver supports in-band dynamic updates of some of the media stream attributes from Media Info Blocks. The info block mechanism is standard for IPMX Senders but it is optional for Receivers. A list of supported Media Info Block types is provided. En empty list indicate that the info block mechanism is not supported at all. A list having only the value 0, which is an invalid media info block type identifier, serves the same purpose. A partial list indicate the Media Info Block types that are supported. When media stream attributes associated with a Sender change, a Controller may let the Receiver handle the media stream attributes changes from the media info blocks produced by the Sender, if all of media info block types produced by a Sender are supported by the Receiver. Note that for coded Flows the Sender `parameter_sets_flow_mode` attribute allows for a similar functionality when the content of the SDP transport file does not change. The `info_block` capability allows for more flexibility when the SDP transport file changes are transmitted as part of the IPMX info block.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** array of integer (Media Info Block type identifiers)
  - **Target:** (a) `transport_file` activation attribute of the Receiver.
- **Applicability:** AMWA IS-04 v1.3, AMWA IS-05 v1.1

### USB Class
- **Name:** `urn:x-matrox:cap:transport:usb_class`
- **Description:** Indicates the USB classes (array of integers in the 0 to 255 range) supported by the USB transport. See [www.usb.org](https://www.usb.org/defined-class-codes) for class codes definitions.
- **Specification:** [Sender Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/SenderCapabilities.md), [Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
  - **Type:** array of integer
- **Applicability:** AMWA IS-04 v1.3

[RFC-4566]: https://tools.ietf.org/html/rfc4566 "SDP: Session Description Protocol"
[RFC-9134]: https://tools.ietf.org/html/rfc9134 "RTP Payload Format for ISO/IEC 21122 (JPEG XS)"
[color-sampling]: https://www.iana.org/assignments/media-type-sub-parameters/media-type-sub-parameters.xhtml#media-type-sub-parameters-15 "Media Type Sub-Parameter Registry for video/raw: Color (sub-)sampling"
