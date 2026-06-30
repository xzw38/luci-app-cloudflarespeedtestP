# luci-app-cloudflarespeedtest

[![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/stevenjoezhang/luci-app-cloudflarespeedtest/build.yml?style=for-the-badge&logo=GitHub)](https://github.com/stevenjoezhang/luci-app-cloudflarespeedtest/actions/workflows/build.yml)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/stevenjoezhang/luci-app-cloudflarespeedtest?style=for-the-badge)](https://github.com/stevenjoezhang/luci-app-cloudflarespeedtest/releases)

[中文说明](README.CN.md)

**luci-app-cloudflarespeedtest** is a LuCI application for OpenWrt, based on the [CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest) core tool. It automatically tests the latency and download speed of Cloudflare IPs, selects the best ones for your network, and updates them to proxy plugins like SSR+ and Passwall.

This project is a fork of [mingxiaoyu/luci-app-cloudflarespeedtest](https://github.com/mingxiaoyu/luci-app-cloudflarespeedtest) with significant refactoring and improvements.

## Features

*   **Auto Speed Test**: Periodically or manually test Cloudflare IPs to find the best one.
*   **Proxy Integration**: Automatically update the best IP to SSR+, Passwall, MosDNS, astra-dns, and other proxy or DNS tools.
*   **Visual Charts**: View history charts for latency and download speed trends.
*   **Auto Core Download**: The package does not contain the core binary; it downloads automatically on the first run, reducing the package size.
*   **Improved UI & Logs**: Redesigned status display and log format for better readability.

## Fork Additions

This fork keeps the original behavior by default and adds an optional Passwall/Passwall2 sequential IP assignment mode.

*   **Sequential Passwall IP Assignment**: When enabled in Third Party Settings, selected Passwall or Passwall2 nodes are filled one by one with the top IPs from the latest speed test results. For example, the 1st selected node receives the 1st-ranked IP, the 2nd selected node receives the 2nd-ranked IP, and so on.
*   **Backward Compatible**: The new option is disabled by default. If it is not enabled, the plugin still writes the single best IP to all selected nodes, exactly like the original behavior.
*   **Automatic Result Count**: When sequential assignment is enabled, the speed test automatically requests at least as many ranked IPs as the number of selected Passwall/Passwall2 nodes. If the final result still contains fewer IPs, the extra nodes are skipped instead of being filled with a duplicate IP.

## Installation

1.  Download the latest `.ipk` or `.apk` file from [Releases](https://github.com/stevenjoezhang/luci-app-cloudflarespeedtest/releases).
2.  Install it on your router:
    ```bash
    opkg install luci-app-cloudflarespeedtest_*.ipk
    ```
3.  Go to LuCI -> Services -> CloudflareSpeedTest to configure.

## Screenshots

![Overview](screenshots/overview.png)
![History Chart](screenshots/chart.png)

## Build

```bash
# Compile package only
make package/luci-app-cloudflarespeedtest/compile V=99

# Compile full image
make menuconfig
#choose LuCI ---> 3. Applications  ---> <*> luci-app-cloudflarespeedtest..... for LuCI ----> save
make V=99
```

## Acknowledgements

*   [CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest)
*   [mingxiaoyu/luci-app-cloudflarespeedtest](https://github.com/mingxiaoyu/luci-app-cloudflarespeedtest)
