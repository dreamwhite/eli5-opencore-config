# Cleaning OpenCore config.plist

The aim of this guide is helping newcomers on the necessary steps to prepare the OpenCore config.plist starting from [Sample.plist](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Sample.plist) **FROM MY POINT OF VIEW** in an analytic way

I'll try to write as much as I can, but feel free of improving this guide with a PR.

# Requirements

- [ProperTree](https://github.com/corpnewt/ProperTree)
- [Sample.plist](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Sample.plist)
- [Debug EFI](https://github.com/utopia-team/opencore-debug/releases/latest)

## Premises

For time saving purposes, with a colleague of mine, we created a [Debug EFI](https://github.com/utopia-team/opencore-debug/releases/latest) that only dumps logs, ACPI tables, PCI devices info and much more.

I won't write here the guide on how to create the same EFI, but the relevant quirks that we enabled are:

- `Misc/Debug/SysReport` set to `true`
- `Misc/Debug/Target` set to `67`

The meaning of this EFI is dumping all the necessary informations that aim helping users starting from a solid base, rather than adding random stuff in their BSP (short form of `Board Support Package` aka `EFI`).

More specifically, the important things to note are:

- `opencore-YY-MM-DD-HHMMSS.txt`
- `SysReport/ACPI` folder
- `SysReport/PCI` folder

We'll look onto them separately and will explain how to interprete them.

## Let's start

When opening `Sample.plist` using ProperTree, under `File` menu, click on `Strip Comments` and `Strip Disabled Entries`. This will remove all the comments and disabled entries (you don't say) and will prepare you to clean your resulting `config.plist`.

<details>
<summary>Screenshots</summary>

`Strip Comments`
![Strip Comments](/.assets/images/before/strip_comments.png)


`Strip Disabled Entries`
![Strip Disabled Entries](/.assets/images/before/strip_disabled_entries.png)
</details>




