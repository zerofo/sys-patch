# sys-patch

A script-like system module that patches fs, es and ldr on boot.

---

## Building

### prerequisites
- install devkitpro

```sh
git clone https://github.com/ITotalJustice/sys-patch.git
cd sys-patch
make
```

---

## What is being patched?

Here's a quick run down of what's being patched

- fs
- es
- ldr

fs and es need new patches after every new fw version.

ldr on the other hand needs new patches after every new atmosphere release. this is due to ldr service being reimplemented by atmosphere. in fw 10.0.0, a new check was added to ofw which we needed to patch out. As atmosphere closely follows what ofw does, it also added this check. This is why a new patch is needed per atmosphere update.

---

## How does it work?

it uses a collection of patterns to find the piece of code to patch. alternatively, it could just use offsets, however this would mean this tool would have to be updated after every new fw update, that's not ideal.

the patches are applied at boot, then, the sysmod stops running. the memory footpint of the sysmod is very very small, only using 16kib in total. the size of the binary itself is only 14kib! this doesnt really mean much, but im pretty proud of it :)

---

## Does this mean i should stop downloading / using sigpatches?

No, i would personally recommend continuing to use sigpatches. Reason being is that should this tool ever break, i likely wont be quick to fix it.

---

## If i am using sigpatches already, is there any point in using this as well?

Yes, in 2 niche cases.

1. A new ldr patch needs to be created after every atosphere update. Sometimes, a new silent atmosphere update is released. This tool will always patch ldr without having to update patches.

2. Building atmosphere from src will require you to generate a new ldr patch for that custom built atmosphere. This is easy enough due to the public scripts / tools that exist out there, however this will always be able to

Also, if you forget to update your patches when you update fw / atmosphere, this sysmod should be able to patch everything just fine! so it's nice to have as a fallback.

---

## My request

This repo is mainly a proof of concept. I would love for someone to build upon this, make it into something bigger / better.

here are a few ideas that i have:
- option to only apply patches when in emunand
- option to load new patterns from file
- make this into a service / overlay
- make homebrew frontend that can update this sysmod, apply patches, all without having to reboot

---

## Credits / Thanks

software is built on the shoulders of giants. this tool wouldn't be possible wthout these people:

- DarkMatterCore
- MrDude
- BornToHonk (farni)
- TeJay
- ArchBox
- Shchmue (lockpick)
- Jakibaki (sys-netcheat)
- SciresM (Atmosphere, hactool, etc)
- Switchbrew (libnx, switch-examples)
- DevkitPro (toolchain)