## CFG Lock

As already explained in the [previous step](/booter/mat_support.md#booter), look in the log file for `CFG Lock` string.

<details>
<summary>Example of log file</summary>

e.g. [OpenCore TXT file](https://github.com/dreamwhite/dell-inspiron-5370-hackintosh/blob/master/Docs/SysReport/opencore-2022-07-05-223221.txt#L30)

```
...
02:237 00:077 OCCPU: EIST CFG Lock 0...
```

If the number right after `CFG Lock` is `0` then CFG Lock is unlocked via BIOS.

Therefore, you can disable the following quirks under `Kernel/Quirks` context:

- `AppleCpuPmCfgLock`
- `AppleXcpmCfgLock`

Please note the majority of motherboards may have CFG Lock locked (`CFG Lock 1` in the log file. In case you wanna unlock it, please take a look at [this guide](https://github.com/dreamwhite/bios-extraction-guide).
