# Project libraries

The schematic and PCB use only the project library below. It is registered in
`sym-lib-table` and `fp-lib-table` at the project root using `${KIPRJMOD}`, so
the project needs no global library setup or PCM installs.

| Path | Contents |
|---|---|
| `esp32-rf-tools.symbols/` | Symbols, one `.kicad_sym` file per symbol (a KiCad 10 library folder) |
| `esp32-rf-tools.pretty/` | Footprints |
| `esp32-rf-tools.3dshapes/` | 3D models, referenced as `${KIPRJMOD}/lib/esp32-rf-tools.3dshapes/...` |
| `licenses/` | License texts that must travel with copied parts (e.g. MIT notices) |

To add a part: copy it from an upstream library into these files, point its 3D
model at `${KIPRJMOD}/lib/esp32-rf-tools.3dshapes/`, and add a row below.

## Provenance

| Part | Upstream | Commit | License | Changes |
|---|---|---|---|---|
| Symbol `ESP32-WROOM-32UE` | [espressif/kicad-libraries](https://github.com/espressif/kicad-libraries) `symbols/Espressif.kicad_sym`, symbol `ESP32-WROOM-E` | `dd76561812ab300351234ba6e0ec1295641796f0` | CC-BY-SA 4.0 (see upstream `LICENSE.md`) | Renamed; Value, Description and Footprint field changed to point at `esp32-rf-tools:ESP32-WROOM-32UE` |
| Footprint `ESP32-WROOM-32UE` | same repo, `footprints/Espressif.pretty/ESP32-WROOM-32UE.kicad_mod` | same | CC-BY-SA 4.0 | 3D model path changed to `${KIPRJMOD}`; resaved in KiCad 10 format |
| 3D model `ESP32-WROOM-32UE.STEP` | same repo, `3dmodels/espressif.3dshapes/ESP32-WROOM-32UE.STEP` | same | CC-BY-SA 4.0 | None |
| Symbol `DLS24035B` | Drawn for this project from Elecrow's published pinout: [product page](https://www.elecrow.com/3-5-inch-480-320-spi-tft-lcd-module-with-ili9488-driver.html) and [MSP3520 user manual](https://www.elecrow.com/download/product/DLS24035B/3.5inch_SPI_Module_User_Manual.pdf) | n/a | Own work | 3.5" ILI9488 SPI TFT with touch. Pins 1–14 follow the module's header; the SD card pads are unnumbered on the module and were numbered 15 SD_CS, 16 SD_MOSI, 17 SD_MISO, 18 SD_SCK here. Footprint field set to `esp32-rf-tools:DLS24035B` |
| Footprint `DLS24035B` | Drawn for this project from the module dimension drawings: LCDwiki [`MSP3520_Size.pdf`](https://www.lcdwiki.com/res/MSP3520/MSP3520_Size.pdf) and Elecrow `3.5inch_SPI_Size.png` (in [`Product_Documentation.zip`](https://www.elecrow.com/download/product/DLS24035B/Product_Documentation.zip)) | n/a | Own work | Seen from the LCD side, origin at pad 1. J2 main header = pads 1–14, J4 SD header = pads 15–18 (J4 order SD_CS, SD_MOSI, SD_MISO, SD_CLK from the module schematic), 2.54 mm pitch, 1.0 mm drills; 4 × 3.2 mm non-plated mounting holes on 92.00 × 49.50 mm. No 3D model |
| Symbol `CC1101` | [cyrozap/KiCad](https://github.com/cyrozap/KiCad) `wireless-modules.lib`, symbol `CC1101-868MHz-Module` (legacy format, converted with `kicad-cli sym upgrade`) | `e0f53f26ef767cff1717acfe13072d833551dae9` | CC0-1.0 | Pinout checked against the module datasheet ([V-Chip VT-CC1101-868M, archived](https://web.archive.org/web/20160418053329/http://www.digirf.com:80/xwfu/2013/4f3751b81deca976.pdf)). Renamed to `CC1101`; `CC1101-915MHz-Module` alias dropped; MISO pin type changed from output to tri-state; CSN renamed `~{CSN}` (active low); Footprint set to `esp32-rf-tools:CC1101`; Datasheet changed to the archived copy (original link is dead); Description, keywords and footprint filter updated |
| Footprint `CC1101` | [cyrozap/KiCad](https://github.com/cyrozap/KiCad) `miscellaneous.pretty/CC1101-868MHz-Module.kicad_mod` | `a2f33d70dc4790a2bbc719e4a2e99f71ffb2dadc` | CC0-1.0 | Renamed to match file name; Value, description and tags set; resaved in KiCad 10 format |
| Symbol `TP4056_Module_Protected` | Drawn for this project from the footprint's pad labels (IN+, IN-, B+, B-, OUT+, OUT-), which match the module silkscreen | n/a | Own work | Pins 1 IN+, 2 IN-, 3 B+, 4 B-, 5 OUT+, 6 OUT-; Footprint field set to `esp32-rf-tools:TP4056_Module_Protected` |
| Footprint `TP4056_Module_Protected` | [kubabuda/misc_footprints](https://github.com/kubabuda/misc_footprints) `misc_footprints.pretty/4056E_LiIon_loader_prot.kicad_mod` | `397c0f163059625bea107abfac1bc410295a0789` | MIT, Copyright (c) 2016 kubabu (full text in `licenses/kubabuda-misc_footprints-MIT.txt`) | Renamed; description, tags and courtyard added; Reference placeholder set to `REF**`; silkscreen removed from pad layers; "microUSB" silkscreen label shortened to "USB" and centred in the connector outline (it overlapped it); pad 4 drill changed from 0.762 to 1.2 mm to match pads 3, 5 and 6; resaved in KiCad 10 format. Replaces the former `TP4056-18650` footprint (ccadic/TP4056-18650, no license) |
| Symbol `NRF24L01_Breakout` | [KiCad symbol library](https://gitlab.com/kicad/libraries/kicad-symbols) `RF.kicad_symdir/NRF24L01_Breakout.kicad_sym` | `485804ab03b415f530dd88224c9b7aafad892de4` | CC-BY-SA 4.0 with the KiCad library exception | Checked against the [Handsontec nRF24L01+PA+LNA datasheet](https://www.handsontec.com/dataspecs/module/NRF24L01+PA.pdf). MISO pin type changed from output to tri-state (avoids ERC output/tri-state warnings on a shared SPI bus); IRQ renamed `~{IRQ}` (active low); Datasheet field changed from the dead Nordic link to the Handsontec PDF; Description and footprint filters extended for the PA+LNA module; Footprint field changed to `esp32-rf-tools:nRF24L01_PA_LNA_SMA` |
| Footprint `nRF24L01_PA_LNA_SMA` | Drawn for this project: pads identical to `nRF24L01_Breakout`; outline from the [Handsontec datasheet](https://www.handsontec.com/dataspecs/module/NRF24L01+PA.pdf) (41 × 15.5 mm) | n/a | Own work | Board end 2.0 mm from the pin 1 column (measured on the module). Header centred across the board and SMA overhang of about 6.7 mm estimated from the datasheet's pinout picture; courtyard covers the SMA connector but not the antenna. No 3D model |
| Footprint `nRF24L01_Breakout` | [KiCad footprint library](https://gitlab.com/kicad/libraries/kicad-footprints) `RF_Module.pretty/nRF24L01_Breakout.kicad_mod` (as installed with KiCad 10.0.6) | `18227ee1af2680cab46c6ed908dd53e9272a6116` | CC-BY-SA 4.0 with the KiCad library exception | 3D model reference removed (no model exists upstream). Replaces the former `NRF24L01Module` footprint (KiCad forum, CC BY-NC-SA 3.0) |

The ESP32-WROOM-32UE footprint also fits the older ESP32-WROOM-32U (same
18 × 19.2 mm outline, same 38 pins plus exposed GND pad 39).
