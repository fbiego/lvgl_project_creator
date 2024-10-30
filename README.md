# Project creator

### Kickstart your LVGL projects with ease!

Accelerate your LVGL development with the Project Creator. Select, configure, and launch your projects in just a few clicks. It works on Windows, Linux, Mac and in VSCode too. More projects are coming soon! 🚀

![Untitled](https://github.com/user-attachments/assets/84871ddb-d096-4f69-a587-63a672bd7658)


## Features
### Just works
Works on any OS, and in VSCode without git or any other extra tools.

### Faster than git clone
Pre-packaged with LVGL, it saves you time by skipping repetitive downloads.

### Tailor to your needs
Customize your project’s initial setup through an intuitive and user-friendly interface.

## Technical overview

### List of projects and project properties

- There are `manifest.json` files in some repositories
- We collect the URL of these manifests [here](https://github.com/lvgl/lvgl-project-creator/blob/master/manifests)
- [This script](https://github.com/lvgl/lvgl-project-creator/blob/master/build_manifest_all.py) concatenates the manifests in [manifest_all.json](https://github.com/lvgl/lvgl-project-creator/blob/master/manifest_all.json)
- `manifest_all.json` is loaded into the project creator app
- The Project Creator clones the repository pointed by the `urlToClone` tag in the manifests
- The Project Creator stores a local copy of LVGL and copies it to the correct location of the cloned project   

### `manifest.json`
The followings describes each field of the `manifest.json` files

- `"name"`: Name of the project as a string, e.g., `"Riverdi STM32U5 Embedded 5”`
- `"maintainer"`: Responsible for the project's maintenance as a string, e.g., `"LVGL"` or `"NuttX"`
- `"hostOperatingsystem"`: Supported host operating systems as a string array, e.g., `"Linux"`, `"Windows"`, or `"MacOS"`
- `"environment"`: Keywords for the environment as a string array, e.g., `["CubeIDE", "LLVM"]`
- `"hardware"`: An object with details about the hardware, which can be omitted for simulator projects.
    - `"chipVendor"`: Name of the chip vendor as a string, e.g., `"STM32"`
    - `"manufacturer"`: Name of the manufacturer as a string; can match `chipVendor` if the same, e.g., `"Riverdi"`
    - `"specs"`: Object describing technical specifications; fields may be omitted or added as needed.
        - `"MCU"`: Part number of the MCU with core type and operating frequency, e.g., `"STM32U599NJH6Q (Cortex-M33, 160MHz)"`
        - `"MPU"`: Type of MPU with core count, type, and operating frequency, e.g., `"2 x 64-bit Arm® (Cortex®-A53, 1.4GHz)"`
        - `"RAM"`: List of internal/external memories, e.g., `"1MB (internal), 16MB (external 16-bit, 200 MT/s)"`
        - `"Flash"`: Internal/external memories, e.g., `"2MB (internal), 64MB (external, OCTOSPI)"`
        - `"GPU"`: e.g., `"Neo-Chrom (GPU2D)"`
        - `"Resolution"`: e.g., `"800x480"`
        - `"Display Size"`: e.g., `"5.0”"`
        - `"Interface"`: e.g., `"RGB LCD"`, or `SPI`
        - `"Color Depth"`: e.g., `"24-bit"`
        - `"DPI"`: Diagonal resolution divided by display size, e.g., `"166 px/inch"`
        - `"Technology"`: `"IPS"` or `"TN"`
        - `"Touch Pad"`: Touchpad type, e.g., `"Capacitive (GT911)"`
- `"description"`: Longer description of the project, ~500 characters.
- `"urlToClone"`: Git URL to clone, e.g., `"https://github.com/lvgl/lv_port_riverdi_stm32u5.git"`
- `"logos"`: Links to SVG logos as an array, e.g., `["https://raw.githubusercontent.com/lvgl/project-creator/master/meta/images/st/logo.svg", "https://raw.githubusercontent.com/lvgl/project-creator/master/meta/images/riverdi/logo.svg"]`
- `"branches"`: Supported branches from which the project can be cloned, e.g., `["release/v9.2", "release/v9.3"]`
- `"getStartedInstructions"`: Instructions to get started in Markdown, e.g., ``"1. Connect the power supply to the POWER header\n2. Install [this](https://some-url)\n3. In a terminal type `./build_all.sh`"``
- `"Settings"`: Description of dynamically created settings as an array of objects. Each settings object includes the following fields:
    - `"type"`: `"dropdown"` or `"always"`
        - if `"type":"dropdown"`
            - `"label"`: Text above the dropdown, e.g., `"Show performance monitor"`
            - `"options"`: Object array for dropdown options, e.g., `[{"name": "Yes", "value": "1"}, {"name": "No", "value": "0", "default": "true"}]`
        - if `"type":"always"`:
            - No settings; execute `"actions"` below
    - `"actions"`: Array of objects describing actions. Each action object can include:
        - Search and replace:
            - `"toReplace"`: Regex for the string to find, e.g., `" *#define LV_USE_PERF_MONITOR .*"`
            - `"newContent"`: Replacement for the `toReplace` string, with `{value}` to insert the dropdown selection `"value"`, e.g., `"    #define LV_USE_PERF_MONITOR {value}"`
        - To append content:
            - `"toAppend"`: Appends this string to the file; useful for adding configs to Kconfig files.
        - `"filePath"`: File for search/replace or append; relative to the project folder, e.g., `"path/to/lv_conf.h"`

For full examples, check out:
- [https://github.com/lvgl/lv_port_pc_eclipse/blob/master/manifest.json](https://github.com/lvgl/lv_port_pc_eclipse/blob/master/manifest.json)
- [https://github.com/lvgl/lv_port_linux/blob/master/manifest.json](https://github.com/lvgl/lv_port_linux/blob/master/manifest.json)
- [https://github.com/lvgl/lv_port_espressif_esp32-s3-lcd-ev-board/blob/master/manifest.json](https://github.com/lvgl/lv_port_espressif_esp32-s3-lcd-ev-board/blob/master/manifest.json)
- [https://github.com/lvgl/lv_port_renesas_ek-ra8d1_gcc/blob/master/manifest.json](https://github.com/lvgl/lv_port_renesas_ek-ra8d1_gcc/blob/master/manifest.json)

## Frequently Asked Questions

### Will you add more projects?
Yes, we have started working on adding the LVGL projects from the major chip vendors’ SDKs and RTOS projects. Stay tuned, hundreds of projects will be available soon.

###  Can I submit my own LVGL project?
You can’t at this moment. We added projects for which we know that they will be maintained either by us or by a mature project or vendor. However if you would like to see a specific board or project, contact us, and we will also contact the related manufacturer or maintainer.

### How can I give feedback and ask for help?
Please use the [Project Creator](https://forum.lvgl.io/c/project-creator) category on our Forum.

### Is this tool open source?
Not yet, but we are considering making it open-source in the near future.
