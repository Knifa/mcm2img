# MCM2IMG

Converts Maxim analog video overlay (for example, Betaflight and iNAV OSD) fonts to desired image format, plus extras.

The Maxim format is documented here: https://www.maximintegrated.com/en/design/technical-documents/app-notes/4/4117.html

Useful for: previewing fonts, converting fonts for use in other applications, etc.

# Usage

## mcm2img

Converts fonts to binaries.

    python3 mcm2img.py mcmfile.mcm font.bin [rawfmt] [R] [G] [B]

Example:

    python3 mcm2img.py betaflight.mcm font.bin RGBA 0 255 0` for green font colour

mcmfile.mcm file can found in the Configurator for your flight controller of choice.

For Betaflight, this is at `betaflight-configurator*\resources\osd\1`


If rawfmt is specified, it's one of the (many) raw bitmap formats supported by Pillow: https://github.com/python-pillow/Pillow/blob/main/src/libImaging/Unpack.c#L1483 . RGBA is probably the most common thing you will want here.

## mcm2template

Converts fonts to a template PNG for editing. Scales up 3x.

    python3 mcm2template.py mcmfile.mcm

## template2img

Converts a template PNG to binaries.

    python3 template2img.py template.png

## template_overlay

Generates a template overlay PNG. Combine this with a template PNG in e.g., GIMP with some alpha so you can see where the grid lies.

    python3 template_overlay.py

# Docker

The docker container will automatically convert all .mcm fonts found in `/app/fonts` with mcm2img.py

## Volumes
| Volume | Path       |
|:-------|-----------:|
| fonts  | /app/fonts |

## Environment variables
| Variable | Comment                                           | Default     |
|:---------|---------------------------------------------------|------------:|
| RGB      | Used to override the colour of the converted font | 255 255 255 |


## Building

To build the docker image locally please use the following command:

    docker build . -t mcm2img:latest

## Running
Copy the font files (.mcm only) somewhere and execute the following command:

    docker run -v ${PWD}/fonts:/app/fonts -it mcm2img:latest
