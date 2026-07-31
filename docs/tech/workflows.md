# ADM WORKFLOWS

There are three obvious workflows for ADM that broadcaster can build-upon.

Step-by-step they also form a gradual way of implementation and adding complexity
when migrating from conventional "legacy" audio production to object-based and NGA delivery

## STAGE 1. ADM*4*Legacy

![](img/ADM-WF-ADM4Legacy-v05.png)

  - ADM MXF (ST2131) contains essential info about contained assets
  - no sidecar file workflows required
  - (semi-)automation possible for all workflows
  - enabling on-air and on-demand delivery with *MULTI-AUDIO*


## STAGE 2. ADM*2*Legacy

![](img/ADM-WF-ADM2Legacy-v05.png)

- ADM applied for genuine object-based mixes
- delivery to conventional, "legacy" audio codecs requires hosted rendering
- benefits are:
     - sources and stems kept seperately (smaller track counts)
     - multiple rendering format as required (2.0, 5.1. 5.1.4, binaural)
     - enabling on-air and on-demand delivery with *MULTI-AUDIO*

## STAGE 3. ADM*2*NGA

![](img/ADM-WF-ADM2NGA-v05.png)

  - ADM applied for genuine object-based mixes
  - sources and stems kept seperately (smaller track counts)
  - enabling conversion into mutliple NGA codecs (AC-4, MPEG-H, Eclipsa)
    as required by platform
  - rendering on NGA capable end-user device allows ultimate personalisation for
    - Speech Intelligibility,
    - Audio Description
    - Immersive Reproduction

    ->The [ADM Studio Set-up](ADM_studio.md) is a paradigmatic implemenation of this stage.
