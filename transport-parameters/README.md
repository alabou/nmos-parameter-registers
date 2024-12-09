# NMOS Transport Parameters
{:.no_toc}

This register contains the names of additional transport parameters that could be included in the objects in an [IS-05](https://specs.amwa.tv/is-05) `transport_params` array.

For historical reasons, these ["externally-defined" parameters](https://specs.amwa.tv/is-05/v1.1.1/docs/4.0._Behaviour.html#externally-defined-parameters) are not URNs, like many other registered parameters.
Instead, they are clearly identified using the prefix `ext_`.

- A markdown unordered list which will be replaced with the ToC, excluding the "Contents header" from above
{:toc}

## Criteria

- Parameter names MUST match the regex pattern `^ext_[a-zA-Z0-9_]+$`, i.e. they start with `ext_` and contain only alphanumeric or underscore characters.
- Each entry MUST have a short description.
- Each entry SHOULD provide a link to a specification where the parameter is defined, as well as identifying any AMWA Specifications and versions for which the entry is applicable.
- Additions and updates to this parameter register are to be submitted via a Pull Request (PR) according to the [General Procedures and Criteria](../common/).

## Values

Note: JSON schemas supporting validation of all the `ext_` transport parameters defined in this register are available as **[sender_transport_params_ext_register.json](sender_transport_params_ext_register.json)**
and **[receiver_transport_params_ext_register.json](receiver_transport_params_ext_register.json)**.
These MAY be used in addition to the transport-specific schemas, such as **sender_transport_params_rtp.json**, found in the AMWA IS-05 specification.

### IS-07 Source ID
- **Name:** `ext_is_07_source_id`
- **Description:** Identifies the Source that emits an IS-07 event.
- **Specification:** [AMWA IS-07 v1.0](https://specs.amwa.tv/is-07/v1.0)
- **Applicability:** AMWA IS-05 since v1.1, IS-07 since v1.0

### IS-07 REST API URL
- **Name:** `ext_is_07_rest_api_url`
- **Description:** URL of the Events API resource providing the current state and type of an Event emitter (Source).
- **Specification:** [AMWA IS-07 v1.0](https://specs.amwa.tv/is-07/v1.0)
- **Applicability:** AMWA IS-05 since v1.1, IS-07 since v1.0

### Link Offset Delay
- **Name:** `ext_link_offset_delay`
- **Description:** Identifies the Link Offset Delay used to synchronise Playout Time of all components of a stream by receivers.
- **Specification:** ST 2110-10:2022 and VSF TR-10-8
- **Applicability:** AMWA IS-05 since v1.1

### Privacy Protocol, Mode, iv, Key Generator, Key Id, Key Version, ECDH Sender Public Key, ECDH Receiver Public Key, ECDH Curve
- **Name:** `ext_privacy_protocol`, `ext_privacy_mode`, `ext_privacy_iv`, `ext_privacy_key_generator`, `ext_privacy_key_id`, `ext_privacy_key_version`, `ext_privacy_ecdh_sender_public_key`, `ext_privacy_ecdh_receiver_public_key`, `ext_privacy_ecdh_curve`
- **Description:** Privacy Encryption Protocol (PEP) parameter as per IPMX TR-10-13
- **Specification:** VSF TR-10-13
- **Applicability:** AMWA IS-05 since v1.1

### audio_layers_mapping, video_layers_mapping, data_layers_mapping
- **Name:** `ext_audio_layers_mapping`, `ext_video_layers_mapping`, `ext_data_layers_mapping`
- **Description:** For a Receiver of format `urn:x-nmos:format:mux`, it indicates, for a given format, the sub-Stream of a multiplexed stream corresponding to a Receiver's sub-Stream layer. It corresponds to a string of coma separated unsigned integer values indicating, for each layer of the Receiver, which sub-Stream of the multiplexed stream provides the essence. The length of the coma separated list MUST be within the min/max range of the `urn:x-matrox:audio_layers`, `urn:x-matrox:video_layers`, `urn:x-matrox:data_layers` capabilities of the Receiver. More precisely for a given *format* it MUST be min(max(sender *format*_layers, receiver *format*_layers_min), receiver *format*_layers_max). An empty string indicates that no re-mapping is to be performed. These attributes are optional and may not be supported as transport parameters in which case no re-mapping is performed. A Controller MUST NOT specify indices of sub-Streams that are not part of the multiplexed stream. For a given format, a Controller MUST NOT duplicate sub-Streams indices.
- **Specification:** [Matrox Receiver Capabilities](https://github.com/alabou/NMOS-MatroxOnly/blob/main/ReceiverCapabilities.md)
- **Applicability:** AMWA IS-05 since v1.1
