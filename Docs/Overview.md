## Pack Content
<!-- Todo: Detailed CMSIS-Pack content list. -->

This board support pack contains the following:

| Content                      | Description |
|------------------------------|-------------|
| ./.github/workflows          | GitHub workflows for building the pack and testing the examples. |
| ./Doc                        | General documentation. |
| ./Doc/ACMEBoardCM4           | Schematics and user guides. |
| ./Drivers                    | [CMSIS-Driver VIO](#drivers). |
| ./Examples/Blinky            | [Blinky](#examples) example. |
| ./Flash                      | Flash programming algorithm for on-board SRAM. |
| ./Images                     | Board photos. |

## Related packs
<!-- Todo: Additional CMSIS-Packs that are required for the contents to work. -->

- [ACME.ACMECM4_DFP.1.1.0.pack](https://www.acme-website.com/pack/ACME.ACMECM4_DFP.1.1.0.pack)

## Examples
<!-- Todo: Description of the example projects provided in the CMSIS-Pack. -->

| Example | Description |
|---------|-------------|
| [Blinky](./Examples/Blinky/Blinky.csolution.yml) | Blinky example to test tools and hardware setup. |
|         |             |

## Layers
<!-- Todo (if available): Description of the csolution layers provided in the CMSIS-Pack. -->

| Layer   | Description |
|---------|-------------|
|         |             |

## Drivers
<!-- Todo: Description of the HAL/CMSIS-Drivers provided in the CMSIS-Pack. -->

| Drivers                                          | Description |
|--------------------------------------------------|-------------|
| [CMSIS-Driver VIO](./Drivers/vio_ACMEBoardCM4.c) | VIO connected to LEDs (X, Y) and USER button (Z) |
|                                                  |             |

## Usage
<!-- Todo: Additional usage information. -->

### Configuration
<!-- Todo: Usage subsection: Description of the configuration options. -->

### Tools or deviations from CMSIS standard
<!-- Todo: Usage subsection: Description of any required tools and deviations from the CMSIS-Pack standard. -->

## Links
<!-- Todo: Useful links with documentation/help/forums. -->

| Link             | Description |
|------------------|-------------|
| [Product page]() | Information regarding the board. |
| [GitHub Repo]()  | Location of the BSP repository. |
| [Support]()      | How to contact support. |
| [User forum]()   | Public user forum. |
