# Booter


It's recommended to check `MAT Support` status as well as `available slides` that your motherboard may require.

To achieve this, you want to check `opencore-YYYY-MM-DD-HHMMSS.txt` file. It can be obtained by using OpenCore `DEBUG` binaries (mainly `OpenCore.efi` and `OpenRuntime.efi`) with logging to file enabled (`Misc/Debug/Target` set to `67`).

### MAT Support

For time saving purposes, with a colleague of mine I created a debug that serves this purpose. You can download it [here](https://github.com/utopia-team/opencore-debug/releases/latest).

When you get `opencore-YYYY-MM-DD-HHMMSS.txt`, look for `MAT Support is` string.

<details>
<summary>Example of log file</summary>

e.g. [OpenCore TXT file](https://github.com/dreamwhite/dell-inspiron-5370-hackintosh/blob/master/Docs/SysReport/opencore-2022-07-05-223221.txt#L79)

```
...
13:350 00:236 OCABC: MAT support is 1
...
```

In the above example, since `MAT Support` is available, you'll tweak your `config.plist` as it follows under `Booter/Quirks` context:

- `EnableWriteUnprotector` set to `false`
- `RebuildAppleMemoryMap` set to `true`
- `SyncRuntimePermissions` set to `true`

##### Please note that on some motherboards, additional steps may be required. More info available [here](https://dortania.github.io/OpenCore-Install-Guide/extras/kaslr-fix.html#using-devirtualisemmio)
</details>
<br>

## Slide values

This step requires a bootable EFI, hence the debug EFI in the above steps cannot be used anymore.

As [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/extras/kaslr-fix.html#so-what-is-kaslr) states:


> Well KASLR stands for Kernel address space layout randomization, what it's used for is security purposes. Specifically, this makes it much harder for attackers to figure out where the important objects are in memory as it's always random both between machines and between boots. More in-depth explainer on [KASLR](https://lwn.net/Articles/569635/)


> Where this becomes an issue is when you introduce devices with either small memory maps or just way too many devices present. There likely is space for the kernel to operate but there's also free space where the kernel won't fit entirely. This is where slide=xxx fits in. Instead of letting macOS choose a random area to operate in each boot, we'll constrain it to somewhere that we know will work.


OpenCore can automatically calculate the right `slide` value, but some motherboards (mainly ASUS and ASRock) may have all the usable slides. Consider yourself lucky in such case.

To check it, with logging to file enabled (`Misc/Debug/Target` set to `67`), look for `OCABC: All slides are usable! You can disable ProvideCustomSlide!` string.

If you find it, then proceed disabling the following quirks unders `Booter/Quirks` context:

- `EnableSafeModeSlide`
- `ProvideCustomSlide`
