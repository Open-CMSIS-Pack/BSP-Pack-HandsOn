# Create a Board Support Pack - Hands-On Example

This repository explains the steps to create a board support pack using the Open-CMSIS-Pack technology. 

The pack contains a development board from the imaginary "ACME Corp.". It contains:
- Source code, libraries, header/configuration files for the underlying hardware and documentation (user manuals, getting started guides, and schematics).
- A CMSIS-Driver VIO for on-baord LEDs
- Flash programming algorithm for external board memory

Content                        | Description
:------------------------------|----------------------------------------
[`gen_pack.sh`](./gen_pack.sh) | Script that builds the pack; refer to [usage information](https://github.com/Open-CMSIS-Pack/gen-pack#get-started) for configuration details.
[`.github/workflows/pack.yaml`](./.github/workflows/pack.yaml)  | GitHub workflow that generates the pack on every commit.

## Benefits of Software Pack Delivery

The CMSIS-Pack technology is available in multiple toolchains. Below is a brief history:

- **2008:** CMSIS-Core has been introduced and [CMSIS](https://arm.com/cmsis) has been since then continuously extended.
- **2012:** CMSIS-Pack has been started to simplify Product Lifecycle Management (PLM) of Keil MDK and improve overall user experience.
- **2014:** CMSIS-Pack is part of Keil MDK for device support, middleware which resulted in higher adoption and lower support.
- **2017:** Eclipse version of the CMSIS-Pack system is integrated in Arm DS and IAR toolchains. Sharing packs across toolchains is now possible.
- **2020:** Discussions with ST and NXP resulted in the [Open-CMSIS-Pack](https://github.com/Open-CMSIS-Pack/) project and the [VS Code](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) integration.

### Benefits for a Board Vendor

- **Connection to users:** as board vendor you control distribution to multiple tools and web portals. For the [Arm pack system](https://www.keil.arm.com/packs/) new releases are scanned once per day, making it available to the entire user base. Documentation links in the software pack let you connect with your users.

- **One way to distribute:** for all relevant toolchains as CMSIS supports Arm Compiler, GCC, and IAR. Software scales to many devices when APIs are applied (as in this example CMSIS-Driver).

- **Reduces support efforts:** as it is easier for customer to use a board in projects. Product Lifecycle Management simplifies updates and notifies users about outdated configuration files and deprecation of products.

>To learn more review the session about [Generating CMSIS-Packs for Boards](https://linaro.atlassian.net/wiki/spaces/CMSIS/pages/tbd).

## Pack Development

The following section explains how to create a pack.

### Tool-Environment (Recommended)

- MDK v5.41 with default installation path (C:\Keil_v5\)
- [CMSIS-Toolbox v2.7.0](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/releases) or higher (update files in C:\Keil_v5\ARM\ctools)
- [VS Code](https://code.visualstudio.com/) with [XML Language Support by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml)

### Steps to Create a Board Support Pack

- **Gather technical details**
  - Gather all technical details of your development board that need to be listed.
  - Create [Flash programming algorithms](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/flashAlgorithm.html) for external memories (if applicable).
- **Organize and create the file list** that will be delivered as Pack
- **Create the [PDSC file](ACME.ACMECM4_BSP.pdsc)** using your favorite editor (we recommend VS Code with XML extension).
- **Validate the software pack** using the `packchk` tool.
- **Create the software pack** using the `gen_pack` library.

> A board support example is explained in this [meeting recording](https://linaro.atlassian.net/wiki/spaces/CMSIS/pages/tbd) starting at xx:xx.

### Local Pack Development

1. Clone this repository (as it serves as a getting started example)
2. Register this pack with `cpackget` via [PDSC file](https://github.com/Open-CMSIS-Pack/cpackget/blob/main/README.md#adding-packs) using this commands:

   ```txt
   cpackget update-index                // optional to ensure that pack index is up-to-date
   cpackget add ACME.ACMECM4_BSP.pdsc   // pack now appears in toolchains, i.e. in MDK
   csolution list packs
   ```

3. The content of the pack can now be seen in the Manage Component dialog of uVision.

For changing the [PDSC file](ACME.ACME_BSP.pdsc) it is recommended to use VS Code with XML extension, but any editor would work.

After modifications to the [PDSC file](ACME.ACME_BSP.pdsc) run `packchk`; include all packs that are required by your software in the validation:

Using **Command Prompt**:

```txt
packchk ACME.ACME_BSP.pdsc -i ACMECM4_DFP.pdsc -i %CMSIS_PACK_ROOT%/ARM/CMSIS/6.1.0/ARM.CMSIS.pdsc
```

Using  **Git Bash** console:

```txt
packchk ACME.ACMECM4_BSP.pdsc -i ACMECM4_DFP.pdsc -i $CMSIS_PACK_ROOT/ARM/CMSIS/6.1.0/ARM.CMSIS.pdsc
```

The pack can be created locally in the directory `output` using **Git Bash**:

```txt
./gen_pack.sh -v
```

### Verify Pack in Tools

To verify the tools such as the [VS Code - Keil Studio Desktop](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) extension, install the pack with: 

```txt
cpackget add ./output/ACME.ACMECM4_BSP.1.0.0.pack
```

>**Notes:**
> - [VS Code - Keil Studio Desktop](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) does not yet support pack installation from local repositories.
> - To continue local pack development, change add a new \<release\> version. During development [semantic version](https://semver.org/) labels to indicate a pre-release may be used as shown below:

```xml
  <releases>
    <release version="1.0.1-rc0">
      Further development
    </release>
    <release version="1.0.0" date="2023-04-22">
      Initial version
    </release>
  </releases>
```

### Pack Creation on GitHub

Once changes are committed the [GitHub Action](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/actions) creates the pack.

### Publish Pack

The pack can be hosted on the [\<url\>](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/blob/main/ACME.ACMECM4_BSP.pdsc#L8) specified in the `*.pdsc` file.

Refer to [Publish a Pack](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/createPackPublish.html) in the Open-CMSIS-Pack specification for further details.

### Issues and Questions

Use [Issues](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/issues) on this GitHub to raise questions or submit problems.

**Happy Packing!**
