# Overall ADM Structure

We'll start by giving a brief introduction to the overall structure of the ADM. The ADM consists of a collection of elements, each of which are used to describe aspects of the audio. Each element is represented by an XML element, and they contain various attributes and sub-elements. The elements are connected to each other via references (except `audioBlockFormat`), as shown in this diagram:

<object data="img/adm_structure.svg" type="image/svg+xml"> </object>

The diagram shows the divide between the content part, the format part and the [BW64](../reference/excursions/bw64_and_adm.md) file. Both the content and format parts make up the ADM metadata that is in XML, and is usually carried within a chunk (the 'axml' chunk) in the BW64 file. The BW64 File part at the bottom contains the 'chna' chunk which is a look-up table connecting the ADM metadata with the audio tracks in the file.

The content part describes the technical content of the audio, such as whether it contains dialogue or a particular language, as well as loudness metadata. The format part describes what sort of channels the audio tracks have and how they are grouped together, for example the left and right channels in a stereo pair. The elements in the content part are generally unique to the audio and the programme, whereas the elements in the format part can be reused.

## Short Glossary

Audio terminology does vary over different environments and standards bodies, so to help clarify the terms the ADM uses, here's a short glossary:

  * __Track__ - A sequence of data representing the audio samples stored in a medium. The metadata includes the format of the data (e.g. PCM).
  * __Stream__ - One or more _tracks_ that can be combined to make a complete set of one or more audio signals. A _stream_ represents either a _channel_ (when it is carrying one audio signal), or a _pack_ (when it is carrying more than one audio signal). The metadata includes the audio codec used to generate the data in the _tracks_.
  * __Channel__ - __(1)__ A mono sequence of audio samples that may have a particular spatial location (e.g. 'front left'), or other audio characteristics. Typical metadata for a channel includes the position of the sound, and loudspeaker it is intended for. __(2)__ Audio that is intended for a particular loudspeaker (see [audio types](../background/audio_types.md) for more detail about channel-based audio).
  * __Block__ - A time-slice of a _channel_ of a particular duration. Metadata in _blocks_ allow __channels__ to vary their properties (such a spatial location) over time.
  * __Pack__ - A group of related _channels_ that ought to be kept to together (e.g. 'stereo').
  * __Programme__ - A complete audio programme that contains everything required to playout. Typical metadata attached to a programme includes its duration and the language it is in. A _programme_ contains one or more _contents_.
  * __Content__ - Part of a programme, for example the dialogue or background music. Typical metadata attached to content includes the language of the dialogue and the type of content (e.g. dialogue or music). _Content_ contains one or more _objects_.
  * __Object__ - __(1)__ A set of _tracks_ of a finite duration with a particular _pack_ and _channel_ configuration. The metadata includes start time and duration. __(2)__ A sound located in a particular location in 3D space (see [audio types](../background/audio_types.md) for more detail about object-based audio).
  * __Static__ - Something that does not change over time. For example, a _static_ _channel_ will contain positional metadata fixed to one location.
  * __Dynamic__ - Something that does change over time. For examples, a _dynamic_ _channel_ will contain positional metadata that describes movement over time.
  * __HOA__ - Higher Order Ambisonics, a scene-based representation of audio (see [audio types](../background/audio_types.md) for more detail).
  * __Binaural__ - Sound intended to be delivered directly to a pair of ears (usually over headphones) that gives the impression of 3D immersion and externalisation (see [audio types](../background/audio_types.md) for more detail about binaural audio).
  * __Matrix__ - _Channels_ that are derived from a combination of other _channels_ via a mathematical matrix operation. For examples, Mid and Side _channels_ are a simple _matrix_ of Left and Right _channels_ (see [audio types](../background/audio_types.md) for more detail about matrix audio).

The diagram below helps illustrate how some of these terms relate to each other in the context of an audio file:

<object data="img/glossary_diag.svg" type="image/svg+xml"> </object>

Here, the example audio file contains four _tracks_ (2x PCM, 2x coded), which are grouped into three _streams_ (2x PCM, 1x coded). The two PCM _streams_ each contain a _channel_ ("Left" and "Right"), which are part of a "Stereo" _pack_. The coded _stream_ contains a _pack_ (a "3.0" layout) of three _channels_. Each of the two _packs_ are the format of _objects_, one being a "Dialogue-1" _object_, and the other a "Music-1" _object_. The diagram also shows that the two _objects_ are covering different time regions of the _tracks_ and _streams_. These two objects are each part of different _contents_ ("Dialogue" and "Music"). The "Main" _programme_ contains these two _contents_.

## Starting Point

Do you read the metadata first to find out what is in the audio, or do you want to check each audio track and find out what the metadata is for it? Well, the ADM allows either of these entry points to be taken. If you want to start with the metadata, then starting at `audioProgramme` and working down from there is the way to go. If you want start with the audio, the you work up from the 'chna' look-up table at the bottom.

For this tutorial we'll start with the format part at the bottom where we work up from the 'chna' table; so, let's follow a worked example in the [next step](format_part.md).
