## NVRAM

This section declares all the variables that will be written in the NVRAM of our motherboard (or `nvram.plist` in case you're using emulated NVRAM). Think of NVRAM as a memory space where macOS will interact with, and write stuff such as SIP status ecc.

It's really important that you understand that `everything you add must be previously deleted`. What does this mean?

Let's write a short ELI5:

> Let's suppose that NVRAM is the game with a cube, a bunch of holes and some geometric shapes that you have to put inside that cube. Idk tf explain this but give a look at this image


![](/.assets/images/misc/eli5_gamecube.jpg)

> Imagine that each hole is a NVRAM variable name and the coloured shape is the NVRAM variable content
> What happens if, for example, the hole is already filled with a previously added shape and you wanna add a new fancy coloured shape? There's no space for it unless you previously remove the old one.


Consequently, OpenCore NVRAM mechanism will work like: if it finds a variable that is declared both in Add and Delete context.

So recap, OpenCore NVRAM mechanism will:

1. delete any declared NVRAM variable under `NVRAM/Delete` context
2. add any declared NVRAM variable under `NVRAM/Add` context

What does this mean? Let's show some pics:

`Sample.plist` has the following `NVRAM` structure:

![nvram_add](/.assets/images/before/legacy_nvram.png)

As you can see there are some NVRAM GUIDs:

- `4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14`
- `4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102`
- `7C436110-AB2A-4BBB-A880-FE41995C9F82`

that declare some variables:

- `DefaultBackgroundColor`
- `rtc-blacklist`
- `boot-args`
- and many more

But in the `Delete` context, not everything is deleted. We'll correct it by making sure that every NVRAM GUID (e.g. `4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14`) contains all the variable declared inside it both in `Add` and `Delete` contexts.

Also, please note that in case you're not in a Legacy setup, you can safely empty `LegacySchema` dict:

<details>
<summary>Before</summary>

![legacy_schema](/.assets/images/before/legacy_nvram.png)
</details>

<details>
<summary>After</summary>

![legacy_schema](/.assets/images/after/legacy_nvram.png)
</details>