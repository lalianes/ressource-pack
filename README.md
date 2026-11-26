# ressource-pack

Server resource pack for a small private Paper 1.21.11 server. It bundles a few
popular vanilla-friendly packs into one download and adds a custom creeper.

Download: see [Releases](https://github.com/lalianes/ressource-pack/releases) (latest: `v14`, pack format 75 / Minecraft 1.21.11).

## Compatibility

| | Supported |
| --- | --- |
| Minecraft | Java Edition 1.21.11 only (`pack.mcmeta`: `min_format` = `max_format` = 75) |
| Bedrock | No. Bedrock uses a different pack format, Geyser players will not get it |
| Server software | Any Java server that can send a resource pack: Vanilla, Paper, Spigot, Purpur, Fabric, NeoForge |
| Without a server | Works too: drop the zip into `.minecraft/resourcepacks` and enable it in the game |

Other versions show the pack as incompatible. You can force it on, but GUI
textures and the enchanted book covers may break, because their file layout
changes between versions.

## What's inside

| Part | What it does | Author | License |
| --- | --- | --- | --- |
| [Default Dark Mode](https://github.com/nebuIr/Default-Dark-Mode) | Dark GUI: inventories, chests, furnaces, menus, buttons, recipe book, plus dark textures for ~60 mods | nebuIr | CC BY-NC-SA 4.0 |
| [Re-covered](https://modrinth.com/resourcepack/re-covered) | Every enchanted book gets its own cover per enchantment (works in vanilla via item model selection) | carl_classic | CC BY-NC-ND 4.0 |
| [Low On Fire](https://modrinth.com/resourcepack/low-on-fire) | Lower fire overlay on screen | Haikis | ARR |
| [Low Shield](https://modrinth.com/resourcepack/low-shield-pack) | Lower shield while blocking | Oculie | ARR |
| [Vocal Villagers](https://modrinth.com/resourcepack/vvi) | 43 extra villager voice lines | Owehttamy | see project page |
| Custom creeper | New creeper texture and a custom fuse sound (below) | lalianes | |

The mod-specific folders (`assets/ae2`, `assets/jei`, ...) only apply when the
matching mod is installed. On a vanilla client they are simply ignored.

## Custom creeper

Creepers get a new texture and their own fuse sound. Everything else about the
creeper behaves like vanilla.

### How the sound works

The creeper's fuse sound (`entity.creeper.primed`) is replaced with
`rucksack:creeper_primed` in `assets/minecraft/sounds.json`.

Minecraft always plays the fuse sound at pitch 0.5, which makes any custom sound
an octave lower and twice as long. The entry sets `"pitch": 2.0`, so the final
pitch is 0.5 × 2.0 = 1.0 and the sound plays as recorded.

```json
"entity.creeper.primed": {
  "replace": true,
  "sounds": [{ "name": "rucksack:creeper_primed", "pitch": 2.0 }],
  "subtitle": "subtitles.entity.creeper.primed"
}
```

The fuse lasts 1.5 seconds, so the sound file is trimmed to 1.25 seconds with no
leading silence. It ends just before the vanilla explosion.

## Server setup (itzg/minecraft-server)

```yaml
RESOURCE_PACK: "https://github.com/lalianes/ressource-pack/releases/download/v14/merged_resource_pack.zip"
RESOURCE_PACK_SHA1: "ff39c02ea7fafe4d1eca2891e16efdc6aa6576fa"
RESOURCE_PACK_ID: "20a806fc-87d2-4bf4-a78f-80c8659e9c54"
RESOURCE_PACK_ENFORCE: "TRUE"
```

Change the SHA1 and the ID with every new release, otherwise clients keep the
cached pack.

## Credits

All bundled packs belong to their authors, see the table above. Please support
them on their project pages.
