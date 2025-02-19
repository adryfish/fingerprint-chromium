# fingerprint-chromium

[中文文档](README-ZH.md)

*A fingerprint browser based on `Ungoogled Chromium`.*

## Installation and Usage

### Download

Please download the version suitable for your system from the links below. Each major version of Chromium is compiled into a corresponding release. Choose the appropriate version for your operating system:

| **Version**      | **Source Code**                                                                                      | **Windows**                                                                                   | **Linux**                                                                                   |
|------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Chrome 132**   | [132.0.6834.159](https://github.com/adryfish/fingerprint-chromium/tree/132.0.6834.159)               | [Installer](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.159-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.159-1.1_windows_x64.zip) | [ 132.0.6834.159-1_linux.tar.xz ](https://github.com/adryfish/fingerprint-chromium/releases/download/132.0.6834.159/ungoogled-chromium_132.0.6834.159-1_linux.tar.xz) |
| **Chrome 131**   | [131.0.6778.264](https://github.com/adryfish/fingerprint-chromium/tree/131.0.6778.264)               | | [ 131.0.6778.264-1_linux.tar.xz ](https://github.com/adryfish/fingerprint-chromium/releases/download/131.0.6778.264/ungoogled-chromium_131.0.6778.264-1_linux.tar.xz) |
| **Chrome 130**   | [130.0.6723.116](https://github.com/adryfish/fingerprint-chromium/tree/130.0.6723.116)               | [Installer](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1.1_windows_x64.zip) | [130.0.6723.116-1_linux.tar.xz](https://github.com/adryfish/fingerprint-chromium/releases/download/130.0.6723.116/ungoogled-chromium_130.0.6723.116-1_linux.tar.xz) |
| **Chrome 129**   | [129.0.6668.100](https://github.com/adryfish/fingerprint-chromium/tree/129.0.6668.100)               | [Installer](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1.1_installer_x64.exe) <br> [ZIP](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1.1_windows_x64.zip) | [129.0.6668.100-1_linux.tar.xz](https://github.com/adryfish/fingerprint-chromium/releases/download/129.0.6668.100/ungoogled-chromium_129.0.6668.100-1_linux.tar.xz) |

---

You can find the compiled versions for each major Chromium release on the GitHub Release page. Download the appropriate file for your platform.

### Build from Source

Refer to the [`ungoogled-chromium`](https://github.com/ungoogled-software/ungoogled-chromium/blob/master/docs/building.md) documentation. Simply replace the `ungoogled-chromium` submodule URL with the `fingerprint-browser` repository URL.

## 📢 Advertisement for Chinese Users

<div style="border: 2px solid #f39c12; padding: 15px; background-color: #fffbe6; border-radius: 10px;">

<b>🌟 EasyChat - Claude Mirror Site</b>

A convenient platform for Chinese users to access Claude's AI services: no registration, direct access, and free to use.

🔗 **Visit now**: [https://easychat.top](https://easychat.top)

</div>


---

## Features

### Fingerprinting Features

| **Fingerprint**                 | **Description**                                                                                          | **Command Line Arguments**                                                      |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **User-Agent**                          | Modify the browser's `User-Agent`, including `navigator.userAgent`, `navigator.platform`, `navigator.userAgentData`, and `Client Hints` | `--fingerprint-platform` <br>`--fingerprint-platform-version` <br>`--fingerprint-brand`(131+) <br>`--fingerprint-brand-version`(131+)                  |
| **Audio**                | Obfuscate or spoof audio fingerprint data                                                                | `--fingerprint` (activated when fingerprint seed is enabled)                    |
| **Plugin**               | Modify plugin-related features                                                                           | `--fingerprint` (activated when fingerprint seed is enabled)                    |
| **Hardware**             | Customize hardware parameters such as CPU cores and memory size                                          | `--fingerprint` <br> `--fingerprint-hardware-concurrency`                       |
| **Font**                 | Modify system font information                                                                           | `--fingerprint` (activated when fingerprint seed is enabled)                    |
| **Canvas Image Data Noise**             | Add noise to canvas image data, modifying up to 10 pixels to interfere with fingerprinting               | `--fingerprinting-canvas-image-data-noise`(131-) <br> `--fingerprint`(132+ effective)                                      |
| **Canvas MeasureText Noise**            | Scale `Canvas::measureText()` output by a random factor between `-0.0003%` and `0.0003%`, recalculated at each document initialization | `--fingerprinting-canvas-measuretext-noise`(131-) <br> `--fingerprint`(132+ effective)       |
| **ClientRects Noise**                   | Scale `getClientRects()` and `getBoundingClientRect()` output by a random factor between `-0.0003%` and `0.0003%`, recalculated at each document initialization | `--fingerprinting-client-rects-noise`(131-) <br> `--fingerprint`(132+ effective)  |
| **WebRTC Policy**                       | Disable non-proxied UDP connections by default, preventing real IP address leaks via WebRTC              | `--disable-non-proxied-udp` (enabled by default)                                |
| **Language Support**                    | Set the browser language and accepted languages                                                          | `--lang` (set browser language) <br> `--accept-lang` (set accepted languages)   |
| **Timezone Support**                    | Set the browser timezone                                                                                 | `TZ` environment variable (e.g., `TZ=Asia/Shanghai`)                            |

---

### Automation Features

**Optimized for automation scenarios, offering the following features:**

1. **Fake Shadow DOM Support**  
   Adds the `fakeShadowRoot` property, equivalent to the `shadowRoot` property, enabling access to Closed Shadow Root for easier automation handling.

2. **Avoid CDP Detection**  
   Prevents Chrome DevTools Protocol (CDP) detection when invoking `Runtime.enable`, enhancing stealthiness for automation tools.

---

### Enabling Fingerprint Features with Command Line Arguments

You can enable or customize fingerprinting and privacy protection features by passing command line arguments when launching the browser:

| **Command Line Argument**                  | **Description**                                                                                  |
|--------------------------------------------|--------------------------------------------------------------------------------------------------|
| **`--fingerprint`**                        | Specify the fingerprint seed (seed). Most fingerprint features are activated when this is set.   |
| **`--fingerprint-platform`**               | Specify the operating system type: `windows`, `linux`, or `macos`.                              |
| **`--fingerprint-platform-version`**       | Specify the operating system version. Defaults to the browser's default version if unspecified. |
| **`--fingerprint-brand`**                  | Specify the browser brand in `User-Agent`.                                                      |
| **`--fingerprint-brand-version`**          | Specify the version for the specified browser brand.                                            |
| **`--fingerprint-hardware-concurrency`**   | Specify the number of CPU cores. If unspecified, this is randomly generated based on the seed.  |
| **`--fingerprinting-canvas-image-data-noise`** | Enable canvas image data noise to interfere with fingerprinting. **(Deprecated in 132+)**                                |
| **`--fingerprinting-canvas-measuretext-noise`** | Enable proportional scaling noise for canvas `measureText()` fingerprints.**(Deprecated in 132+)**                     |
| **`--fingerprinting-client-rects-noise`**  | Enable proportional scaling noise for `getClientRects()` and `getBoundingClientRect()`. **(Deprecated in 132+)**         |
| **`--disable-non-proxied-udp`**            | Specify WebRTC policy. Default: disable non-proxied UDP connections (recommended to leave unset).|
| **`--lang`** <br> **`--accept-lang`**      | Set the browser language.                                                                       |

### **New Command Line Arguments for User-Agent Customization**

Chrome 131 introduces two new command line arguments for advanced customization of `User-Agent` and `User-Agent Data`:

- **`--fingerprint-brand`**
  - Specifies the browser brand for `User-Agent` and `User-Agent Data`.
  - Supported values: `Chrome`, `Edge`, `Opera`, `Vivaldi`, or a custom brand name.

- **`--fingerprint-brand-version`**
  - Specifies the version number for the specified brand.
  - Defaults exist for `Chrome`, `Edge`, `Opera`, and `Vivaldi`, but you can provide custom versions.

These arguments enhance browser environment simulation for automation and testing. If `--fingerprint-brand` is omitted, the default brand is used.

## Credits

 * [Ungoogled Chromium](https://github.com/ungoogled-software/ungoogled-chromium)

 ## License

BSD-3-clause. See [LICENSE](LICENSE)