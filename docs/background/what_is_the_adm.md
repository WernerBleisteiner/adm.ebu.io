# What is ADM?

Before we can start using the Audio Definition Model (ADM), we need to know what it is, and also what it is not. The main clue is in its name – it is a model for defining audio. OK, that doesn't really help that much, so let's start with a little history lesson.

## A Brief History

Audio is becoming more complex these days and will continue to do so in the future. In the past we started with mono, and everything was simple. Stereo then came along and then we started to worry about getting the left and right channels round the right way, but it was still pretty straightforward. Then surround sound came along and it started to get tricky. The 5.1 system seemed to have more than one convention for ordering the channels, and then it really started to get tricky. But it didn't end there, as 6.1, 7.1, etc. started appearing and in different flavours, and getting the correct signal to the appropriate speaker turned into a confusing mess. So as sound became more immersive, the complexity increased.

On top of all that, we started to see the potential for content to be delivered in a more personalised way, where additional channels such as Audio Description were introduced, or alternative mixes were offered (such as sport with different commentary).

It started to become clear to handle all these extra channels and complexity each audio channel would need clear labelling. If we could attach this label to the audio channel, then whatever is handling it would know what to do with it. We didn't have to be tied to a particular channel ordering, or fixed configurations.

This leads us on to defining the term 'object-based audio'. Those channel labels are metadata, and when we attach that metadata to some audio, it becomes object-based audio. So as long as we keep this metadata tied to the audio it is describing, we should be able to handle that audio correctly. However, it does mean we need to carry the metadata with the audio. So, this becomes our first definition of what object-based audio is (yes, I did say first, there's another definition coming along later...)

Audio experts started to come up with other techniques (or reviving older techniques) for representing immersive audio. Higher Order Ambisonics (HOA), more generally called scene-based audio, got revived and refined and the audio channels for these formats required labelling. Another approach came along called object-based audio (yes, this is the second definition of this; another name should have been used!), where each audio channel has some positional properties attached to it. These positional properties can then be interpreted by a renderer which attempts to position the sounds in space within the limitations of the location of the speakers. These approaches also removed the need for speakers to be located in locations tied to particular channels. Consequently, the metadata attached to scene and object-based audio is vital for them to be handled correctly.

## Speaking the Same Language

Now that we've introduced metadata to describe the audio, we need to ensure everything can read it. Imagine you just bought a gadget and you want to read the instructions. You can only understand Norwegian, but the instruction manual is in Chinese, so you're stuck. If we insisted all instruction manuals are in Norwegian, then that would fix your problem. But what about those who can't understand Norwegian? Well the bad news for them, is that everyone will have to learn Norwegian. OK, that sounds tough, but at least everyone will understand those instructions.

Of course, when it comes to metadata, it doesn't involve people having to learn a foreign language, but computers understanding a basic format of data. We want to avoid lots of different metadata formats and having to convert between them, particularly if the meaning of the metadata gets lost or misinterpreted. If audio metadata comes in a single openly-published format, then everything can understand it, so it can be easily exchanged. This is where the ADM comes in, it provides a single defined model for the audio metadata that can be understood by everything.

## The Model, a Format and Flexibility

The ADM, as its name suggests, is a conceptual model. To elaborate, it describes set of elements that contain parameters, and their relationships to each other. For example, there is an element that describes an audio channel, and this contains parameters such as the name of the channel. It is also referenced by another element that described a group of channels (called a pack).

So how is this model represented? The ADM primarily uses [XML](https://www.w3schools.com/xml/) which very widely used and human readable. An ADM element is represented by an XML element, with its parameters specified either using attributes or sub-elements.

Looking at the history of audio, we can see that things are changing fast with more complex configurations and systems being introduced. The ADM aims to be able to be future-proof to provide enough flexibility in its design to not limit the size and scope of definitions. It also aims to be easily extended in the future where new parameters can be added without breaking the structure or backwards compatibility.

## What the ADM does and doesn't do

The ADM is used to describe what the audio is, whether it is the purely technical aspect of (e.g. a sound placed such-and-such a position), or fundamental aspects of its content (e.g. contains dialogue in French). This information can be used for processors, such a [renderer](rendering.md) to either generate more usable audio signals (such as direct speaker channels), or decide which channels to keep (e.g. when selecting different language channels). What the ADM does not do is to describe the process itself, so it doesn't tell you how to do the rendering, but rather what you need to render with and what the renderer ought to achieve.
