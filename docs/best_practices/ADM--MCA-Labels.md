#### CONTENT KIND ADM LABELS

To describe specific content types (e.g. *Complete Main*, *Music & Effects*, *Audio Description Mix* etc.), certain attributes are defined in ADM for <audioContent\> components. In the [*ADM4Legacy* (*Step 1*)](/docs/tech/migration.md##STEP-1.-ADM*4*Legacy) use case, with a strict 1:1 relationship between <audioProgramme\> and <audioConten\>, these are directly referenced.     
Here's an overview of the most commonly applied types (pinted in **bold**)

Reference: [ITU-R BS.2076-3](https://www.itu.int/dms_pubrec/itu-r/rec/bs/R-REC-BS.2076-3-202502-I!!PDF-E.pdf) §5.7.3

|   **TYPE**  | **CODE** (within block `<audioContent>. . .</audioContent>`|**German Terms**|
--------------|----------------------------------------------------|-----------------------|
**COMPLETE MAIN (mixed)**|  `<dialogue mixedContentKind="1“>2</dialogue>`  |Sendeton/Standard  |        
Undefined |`<dialogue nonDialogueContentKind="0">0</dialogue>`| Unbekannt|
**Music & Effects** | `<dialogue nonDialogueContentKind="3“>0</dialogue>`  |IT/ME (Musik & Effekte) |
Mixed "Bed" (unspec. *mixed*)  | `<dialogue mixedContentKind="2">2</dialogue>`| BED ( unspec.)   |       
**AD/VI** (*mixed*)       | `<dialogue mixedContentKind="4“>2</dialogue>`  |Audiodeskription (mixed)|     
**Clear Speech** (*mixed*)  | `<dialogue mixedContentKind="3“>2</dialogue>`  |Klare Sprache (mixed)|    
Music (only)  | `<dialogue nonDialogueContentKind="1“>0</dialogue>` |Musik (allein)|    
Effects (only)| `<dialogue nonDialogueContentKind="2“>0</dialogue>` |Effekte (allein)|    
Dialogue (only)|   `<dialogue dialogueContentKind="1“>1</dialogue>` |Sprache/Dialog (allein)|    
Voice over (only)| `<dialogue dialogueContentKind="2“>1</dialogue>` |Übersetzung (allein)|    
Spoken Subtitles (only)| `<dialogue dialogueContentKind="3“>1</dialogue>`|Gesprochene Untertitel (allein)|   
AD (only)|         `<dialogue dialogueContentKind="4“>1</dialogue>` |Audiodeskription (allein)|    
Commentary (only)| `<dialogue dialogueContentKind="5“>1</dialogue>` |Kommentar (allein)|    
Emergency (only)| `<dialogue dialogueContentKind="6“>1</dialogue>` |  Notfallansage|
*<span style='color: red;'>TBD: AmbienceCameraSound*    |   *`<dialogue nonDialogueContentKind="4“>0</dialogue>`*| <span style='color: red;'>*Atmo/Kameraton*  |

### CONTENT KIND MCA LABELS

If applied this is applied in MXF OP1-A using [SMPTE ST 2131](https://pub.smpte.org/doc/st2131/), additional singalling of MCA labels is recommended.    
This table provides an overview how to describe conten types with MCA properties.

Reference: [SMPTE-ST377-41-2023](https://pub.smpte.org/doc/st377-41/20230413-pub/)    

|   **TYPE**  |**German Terms**|  MCA CONTENT | MCA SYMBOL| MCA USE CLASS|
--------------|----------------|--------------|-----------|--------------|    
**COMPLETE MAIN (mixed)**| Sendeton/Standard  | Primary| PRM |FCMP |     
Undefined | Unbekannt| n/a | n/a | n/a |     
**Music & Effects** |IT/ME (Musik & Effekte) | Music & Effects | ME | ICMP  |
Mixed "Bed" (unspec. *mixed*)  |BED ( unspec.)   | n/a | n/a | ?? |      
**AD/VI** (*mixed*)       | Audiodeskription (mixed)| Descriptive Video | DV | FCMP |    
**Clear Speech** (*mixed*)  | Klare Sprache (mixed)| Hearing Impaired | HI | ??   
Music (only)  | Musik (allein)| Music | MX | ICMP |   
Effects (only)| Effekte (allein)| Effects/Foley | FX/FOL | ICMP |
Dialogue (only)|  Sprache/Dialog (allein)| Dialogue | DX | ICMP |    
Voice over (only)| Übersetzung (allein)| Voice-Over | VO | SING |   
Spoken Subtitles (only)| Gesprochene Untertitel (allein)|  n/a | n/a | n/a |
AD (only)|Audiodeskription (allein)| Visually Impaired | VI | SING |   
Commentary (only)|Kommentar (allein)| Recorded Commentary | CM | SING |    
Emergency |  Notfallansage| n/a | n/a | n/a |
 (Silence) |  (Stille) | Silence | MOS | FCMP/SMPL |

Note: MCA Content Labels do not conider "objects" - only composites and elements.
To distinguish these it defines USE Classes    

|     MCA use Class  | Symbol | Definition |
---------------------|--------|------------|
Finished Composite   | FCMP   |The associated MCA Content is a composite, complete work and need not be mixed prior to presentation. It can be mixed with other Soundfield Groups to create other particular desired content per the allowed combinations in Table 4.|
Intermediary Composite| ICMP  |The associated MCA Content is a composite but requires mixing with other elements prior to presentation. It can be mixed with other Soundfield Groups to create desired FCMP content per the allowed combinations in Table 4.|
Simplified           | SMPL  | The associated MCA Content contains a simplified mix, typically mono, stereo or Lt-Rt, intended for special uses. It can be mixed with other SMPL Soundfield Groups to create desired SMPL content per the allowed combinations in Table 4.|
Singular             | SING  | Element contains a single content (such as narration voice) that can be output on its own or be mixed with other Soundfield Groups.|

Therefore, the MCA Content label descriptors have limited correspondences with the object-based concept of ADM.

##### EXAMPLE
The test vector 1.1.6 in the 1st ADM Plugfest (ADM-IG June 2026) was modelled similar to a typical "ADM4Legacy" use case containing different channel-based mixes:
    -Complete Main (Sendeton) 2.0
    -Music & Effects (IT(ME) 2.0
    -Audio Description Mix (AD) 2.0
    -Original Version (OV) 2.0
    -Complete Main (Sendeton) 5.1

The mca-label.txt filecreated for the conversion/muxing of the BW64-ADM.wav in [BMX tool for MXF](https://github.com/ebu/bmx) contained

```
0
# audioProgramme_1
ADM, chunk_id=axml, RFC5646SpokenLanguage="de-DE", MCATitle="MAIN_MIX_2.0-SENDETON_GER", MCATitleVersion="n/a", MCAContent="PRM", MCAUseClass="FCMP", ADMAudioProgrammeID="APR_1001"
# audioProgramme_2
ADM, chunk_id=axml, MCATitle="IT/ME 2.0", MCATitleVersion="n/a", MCAContent="ME", MCAUseClass="FCMP", ADMAudioProgrammeID="APR_1002"
# audioProgramme_3
ADM, chunk_id=axml, RFC5646SpokenLanguage="de-DE", MCATitle="AD-MIX_2.0", MCATitleVersion="n/a", MCAContent="DV", MCAUseClass="FCMP", ADMAudioProgrammeID="APR_1003"
# audioProgramme_4 - It is unclear, if the 'MCA Spoken Language Attribute' "ORIGINAL" is correct?
ADM, chunk_id=axml, RFC5646SpokenLanguage="en-GB", MCATitle="n/a", MCATitleVersion="n/a", MCAContent="PRM", MCAUseClass="FCMP", MCASpokenLanguageAttribute="ORIGINAL", ADMAudioProgrammeID="APR_1004"
# audioProgramme_5
ADM, chunk_id=axml, RFC5646SpokenLanguage="de-DE", MCATitle="MAIN_MIX_5.1-SENDETON_GER", MCATitleVersion="n/a", MCAContent="PRM", MCAUseClass="FCMP", ADMAudioProgrammeID="APR_1005"
```

Note: MCA labels require RFC5646 [IETF language tags](https://datatracker.ietf.org/doc/html/rfc5646)




 The final CL was

 ```raw2bmx -t op1a -o hessischer_rundfunk_1_2_6__test_i4b_adm_A.mxf --audio-layout adm --track-mca-labels x mca-ADM-label-PF26-TV_1_1_6.txt --adm-wave-chunk axml,urn:smpte:ul:060e2b34.0401010d.04020211.02020000 --wave hessischer_rundfunk_1_1_6_test_i4a_adm_A.wav```

 The `urn:smpte:ul:060e2b34.0401010d.04020211.02020000` refers to SMPTE Registry

 ```
 <Entry>
   <Register>Labels</Register>
   <NamespaceName>http://www.smpte-ra.org/reg/400/2012</NamespaceName>
   <Symbol>ADM_ITU2168_Emission_V1_L1</Symbol>
   <UL>urn:smpte:ul:060e2b34.0401010d.04020211.02020000</UL>
   <Kind>LEAF</Kind>
   <Name>ITU-R BS.2168 ADM Emission Profile Version "1", Level "1"</Name>
   <Definition>Identifies the ADM and S-ADM profile identified by profile="ITU-R BS.2168", profileName="Advanced sound system: ADM and S-ADM profile for emission", profileVersion="1", profileLevel="1"</Definition>
   <Applications>ADMProfileLevel</Applications>
   <DefiningDocument>ITU-R BS.2168</DefiningDocument>
   <IsDeprecated>false</IsDeprecated>
 </Entry>
 ```
