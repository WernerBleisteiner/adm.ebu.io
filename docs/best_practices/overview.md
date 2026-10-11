# ADM Best Best Practices: Overview


## Containers and Wrappers for ADM/S-ADM

- **RIFF** audio files, i.e. BWF, RF64 and BW64, store ADM in the <axml\> and <chna\> chunks.  

- In **MXF OP1-A**, **RIFF** audio files can be wrapped using the SMPTE [ST 2131](https://pub.smpte.org/doc/st2131/).

- **IMF**, the most advanced delivery format at present, allows 'compositions' to be created from multiple *MXF* and *BWF* audio and video files, allowing for flexible management of multiple content versions. ADM and S-ADM are wrapped in *MXF* for inclusion in IMF 'compositions'.

See the subsections here to explore how to get the most out with ADM in these typical broadcast production and delivery workflows.


## Descriptors for Content Kind and composites

Typically, audio composits or "mixes" are defined as a certain kind : 
- Complete Main
- Music & Effects
- Audio Description 
- etc.

ADM, for the first time,  allows to assign and carry this information, storing it within the essence itself, the <axml\> chunk within the *BW64*.     
MCA offers a similar technique within the header of a *MXF*.    

The subsection explains and shows examples how to apply both.

