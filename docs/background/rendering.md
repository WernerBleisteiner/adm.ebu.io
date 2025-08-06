# Rendering

With object-based audio, where you have positional metadata attached to audio channels, you need something that processes this metadata and audio and converts them to audio signals that can be sent to conventional channels that eventually feed loudspeakers. This process is called rendering, and the processor is called a renderer.

A renderer receives audio and metadata, as well as information about the desired output format (usually a loudspeaker layout), and interprets the metadata to process the input audio channels in a way that generates the sounds described by the metadata.

For object-based audio (that is where the metadata is describing the positions of the audio objects), a renderer is always required if the audio signals are to be listened to with the correct spatial positioning (otherwise all the channels would just be treated as mono signals). Scene-based audio also requires rendering, and this may just be a conventional HOA decoder, or something more sophisticated. Channel-based audio may not need rendering, particularly if the channels presented match the speaker layout used; however, rendering can be used if the input channel configuration doesn't match the speaker layout. Downmixing can be considered to be a simple form of rendering.

Rendering does not just have to be for generating signals for speaker outputs, as binaural renderers have also been developed to allow to immersive audio to be listened to over headphones. Rendering could also be used for generating general channel, HOA or object-based outputs too (for example when trying to reduce the number of tracks or objects in a file).

## Available Renderers

If we want to listen to audio that has ADM metadata accompanying it, then we'll need a renderer. Fortunately, the EBU have developed the [EAR](https://github.com/ebu/ebu_adm_renderer) (EBU ADM Renderer), which is an open-source renderer written in Python. It has been designed to be a baseline reference for rendering from ADM metadata, and to be simple to use.

Other renderers have been developed, including one in the MPEG-H decoder. This renderer has been designed around the MPEG-H metadata structure, and can handle both object and scene-based audio. Dolby and DTS have also developed renderers designed to work with their immersive audio systems.

All these renderers use slightly different algorithms internally, so may produce subjectively different sounding outputs. In the future, more rendering algorithms may come along that provide improved performance and greater flexibility.
