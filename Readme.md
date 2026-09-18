# OverEnchant Wiki

OverEnchant is a lightweight item customization plugin for modern Paper and Folia servers.

It allows you to apply vanilla enchantments above their normal limits, create fully formatted item names and lore, and configure how the plugin gives feedback to players using chat, action bars, titles, boss bars, sounds and particles.

---

## Features

OverEnchant includes:

```text
Over-level vanilla enchantments
Custom item names
Full lore editing
MiniMessage formatting
Gradients and HEX colors
Optional legacy color support
Configurable Chat feedback
Configurable ActionBar feedback
Configurable Title feedback
Configurable BossBar feedback
Configurable sounds
Configurable particles
Editable language files
Paper support
Folia support
Single Universal JAR
```

---

## Commands

```text
/overenchant
/oe
```

Shows the OverEnchant help menu.

```text
/oe enchant <enchantment> <level>
```

Applies a vanilla enchantment to the item in your main hand.

Example:

```text
/oe enchant sharpness 10
/oe enchant minecraft:sharpness 255
```

By default, OverEnchant allows enchantment levels from `1` to `255`.

---

```text
/oe name <text>
```

Changes the name of the item in your main hand.

Example:

```text
/oe name <gradient:#875CFF:#FF67D4><bold>Legendary Sword</bold></gradient>
```

To remove the custom name:

```text
/oe name clear
```

The default clear keywords are:

```text
clear
reset
remove
```

---

## Lore Commands

Add a new lore line:

```text
/oe lore add <text>
```

Example:

```text
/oe lore add <gray>A weapon forged beyond vanilla limits.</gray>
```

Edit an existing lore line:

```text
/oe lore set <line> <text>
```

Example:

```text
/oe lore set 1 <yellow>My first lore line</yellow>
```

Insert a new line at a specific position:

```text
/oe lore insert <line> <text>
```

Remove a lore line:

```text
/oe lore remove <line>
```

Remove all lore:

```text
/oe lore clear
```

List the current lore lines:

```text
/oe lore list
```

---

## Lore Shortcuts

OverEnchant also includes shorter versions of the lore commands.

```text
/oe add <text>
/oe set <line> <text>
/oe insert <line> <text>
/oe remove <line>
/oe clear
/oe list
```

Example:

```text
/oe add <gradient:#55D6FF:#9A76FF>Upgradeable Item</gradient>
```

---

## Languages

Available languages:

```text
en
it
es
fr
```

Change the active language with:

```text
/oe lang <language>
```

Examples:

```text
/oe lang en
/oe lang it
/oe lang es
/oe lang fr
```

Language files are stored in:

```text
plugins/OverEnchant/languages/en.yml
plugins/OverEnchant/languages/it.yml
plugins/OverEnchant/languages/es.yml
plugins/OverEnchant/languages/fr.yml
```

These files are the source of truth for plugin messages.

There is no active `messages.yml` file.

If you edit the currently selected language file, OverEnchant can automatically reload the changes when language hot reload is enabled.

You can also reload everything manually with:

```text
/oe reload
```

Example:

```yaml
language: en

languages:
  hot-reload: true
  hot-reload-check-interval-ms: 750
```

---

## Formatting

OverEnchant supports MiniMessage formatting in item names, lore and configurable feedback messages.

### Basic Colors

```text
<red>Red Text</red>
<green>Green Text</green>
<gold>Gold Text</gold>
<aqua>Aqua Text</aqua>
```

### Bold and Other Decorations

```text
<bold>Bold Text</bold>
<italic>Italic Text</italic>
<underlined>Underlined Text</underlined>
<strikethrough>Strikethrough Text</strikethrough>
```

### HEX Colors

```text
<#875CFF>Purple Text</#875CFF>
```

### Gradients

```text
<gradient:#875CFF:#FF67D4><bold>OverEnchant</bold></gradient>
```

Example item name:

```text
/oe name <gradient:#875CFF:#FF67D4><bold>Celestial Blade</bold></gradient>
```

Example lore:

```text
/oe add <gray>Forged with</gray> <gradient:#55D6FF:#9A76FF>forbidden magic</gradient>
```

---

## Legacy Color Support

Legacy color formats can also be enabled or disabled in `config.yml`.

```yaml
formatting:
  legacy-ampersand: true
  legacy-section-sign: true
  legacy-hex: true
  disable-default-italic-on-items: true
```

Examples:

```text
&cRed Text
&lBold Text
&#875CFFHex Text
```

Bungee-style legacy HEX formatting is also supported when legacy HEX support is enabled.

---

## Enchantment Settings

The default enchantment configuration is:

```yaml
enchant:
  minimum-level: 1
  maximum-level: 255
  ignore-vanilla-level-limit: true
  allow-incompatible-items: true
  accept-default-minecraft-namespace: true
```

### Maximum Enchantment Level

Change the maximum allowed level:

```yaml
enchant:
  maximum-level: 255
```

Example:

```text
/oe enchant sharpness 255
```

### Vanilla Level Limits

To force vanilla enchantment level limits:

```yaml
enchant:
  ignore-vanilla-level-limit: false
```

### Incompatible Items

By default, OverEnchant can apply enchantments to items that vanilla normally rejects.

```yaml
enchant:
  allow-incompatible-items: true
```

Set it to `false` to restore vanilla compatibility and conflict checks.

### Minecraft Namespace

This option allows both:

```text
sharpness
```

and:

```text
minecraft:sharpness
```

Configuration:

```yaml
enchant:
  accept-default-minecraft-namespace: true
```

---

## Name Settings

Default name settings:

```yaml
name:
  maximum-plain-length: 256
  allow-empty: false
  clear-keywords:
    - clear
    - reset
    - remove
```

You can add or remove clear keywords from this list.

---

## Lore Settings

Default lore settings:

```yaml
lore:
  maximum-lines: 100
  maximum-plain-line-length: 512
  line-numbers-start-at: 1
```

Example:

```yaml
lore:
  maximum-lines: 50
  maximum-plain-line-length: 300
  line-numbers-start-at: 1
```

---

## Feedback System

OverEnchant allows every main operation to have its own feedback configuration.

Available profiles:

```text
feedback.enchant
feedback.name
feedback.lore
feedback.language
feedback.reload
```

Each profile can independently use:

```text
Chat messages
Chat display
ActionBar
Title + Subtitle
BossBar
Sound
Particles
```

Supported display types:

```text
NONE
CHAT
ACTIONBAR
TITLE
BOSSBAR
```

Only one `display.type` is used by a profile at a time.

The normal translated success message is controlled separately by:

```yaml
chat-messages: true
```

This means you can, for example, show both the normal success message in chat and a BossBar at the same time.

---

## ActionBar Example

```yaml
feedback:
  enchant:
    chat-messages: true

    display:
      enabled: true
      type: ACTIONBAR
      message: ''
      message-key: feedback.enchant.message
      duration-ms: 1800

    sound:
      enabled: true
      key: minecraft:block.enchantment_table.use
      source: player
      volume: 0.85
      pitch: 1.20

    particles:
      enabled: true
      type: ENCHANT
      count: 35
      offset-x: 0.45
      offset-y: 0.65
      offset-z: 0.45
      speed: 0.08
      y-offset: 1.00
```

When an enchantment is applied, the configured message appears in the player's ActionBar.

---

## BossBar Example

```yaml
feedback:
  enchant:
    chat-messages: true

    display:
      enabled: true
      type: BOSSBAR
      message: '<gradient:#875CFF:#FF67D4><bold>ENCHANTED</bold></gradient> <white><enchantment> <level></white>'
      message-key: feedback.enchant.message
      duration-ms: 1800

      bossbar:
        color: PURPLE
        overlay: PROGRESS
        progress: 1.0
```

Supported BossBar colors:

```text
PINK
BLUE
RED
GREEN
YELLOW
PURPLE
WHITE
```

Supported BossBar overlays:

```text
PROGRESS
NOTCHED_6
NOTCHED_10
NOTCHED_12
NOTCHED_20
```

Example with a segmented BossBar:

```yaml
bossbar:
  color: PURPLE
  overlay: NOTCHED_10
  progress: 1.0
```

---

## Title Example

```yaml
feedback:
  lore:
    chat-messages: false

    display:
      enabled: true
      type: TITLE
      message: '<gradient:#5CFFB0:#55D6FF><bold>LORE UPDATED</bold></gradient>'
      message-key: feedback.lore.message
      subtitle: '<gray>Your item lore has been changed.</gray>'
      subtitle-key: feedback.lore.subtitle
      duration-ms: 1600

      title:
        fade-in-ms: 150
        stay-ms: 900
        fade-out-ms: 250
```

---

## Chat Display Example

To use the configurable display itself as a chat message:

```yaml
feedback:
  name:
    chat-messages: false

    display:
      enabled: true
      type: CHAT
      message: '<gradient:#55D6FF:#9A76FF><bold>NAME UPDATED</bold></gradient>'
      message-key: feedback.name.message
```

If `chat-messages` is also `true`, the normal translated success message will also be sent.

---

## Disable Visual Feedback

To disable the extra display completely:

```yaml
display:
  enabled: false
  type: NONE
```

You can still keep sounds, particles and the standard chat message enabled.

---

## Language-Based Feedback Messages

You do not need to hardcode feedback text inside `config.yml`.

If this is empty:

```yaml
message: ''
```

OverEnchant uses the configured language key:

```yaml
message-key: feedback.enchant.message
```

For example, inside `languages/en.yml`:

```yaml
feedback:
  enchant:
    message: '<gradient:#875CFF:#FF67D4><bold>OVERENCHANTED</bold></gradient> <dark_gray>•</dark_gray> <white><enchantment> <level></white>'
    subtitle: '<gray>Enchant applied successfully.</gray>'
```

You can customize each language independently.

For example, inside `languages/es.yml`, edit the Spanish message and then use:

```text
/oe reload
```

or leave language hot reload enabled.

---

## Feedback Placeholders

Feedback messages can use placeholders provided by the current operation.

For enchantment feedback:

```text
<enchantment>
<level>
```

Example:

```yaml
message: '<green>Applied <white><enchantment> <level></white>.</green>'
```

For language feedback:

```text
<language>
```

The language files also support:

```text
<prefix>
```

which is replaced by the configured language prefix.

---

## Sounds

Every feedback profile can play a sound.

Example:

```yaml
sound:
  enabled: true
  key: minecraft:block.enchantment_table.use
  source: player
  volume: 0.85
  pitch: 1.20
```

Available sound sources include:

```text
master
music
record
weather
block
hostile
neutral
player
ambient
voice
```

Another example:

```yaml
sound:
  enabled: true
  key: minecraft:ui.button.click
  source: master
  volume: 0.70
  pitch: 1.20
```

---

## Particles

Every feedback profile can also spawn particles around the player.

Example:

```yaml
particles:
  enabled: true
  type: ENCHANT
  count: 35
  offset-x: 0.45
  offset-y: 0.65
  offset-z: 0.45
  speed: 0.08
  y-offset: 1.00
```

Another example:

```yaml
particles:
  enabled: true
  type: END_ROD
  count: 12
  offset-x: 0.30
  offset-y: 0.50
  offset-z: 0.30
  speed: 0.02
  y-offset: 1.00
```

Particles that require additional Bukkit particle data are not supported by the generic feedback system and are skipped safely.

OverEnchant also includes compatibility handling for particle names that changed between older and newer Minecraft versions.

---

## Complete Feedback Example

This example uses a BossBar, chat message, sound and particles when an enchantment is applied:

```yaml
feedback:
  enchant:
    chat-messages: true

    display:
      enabled: true
      type: BOSSBAR
      message: '<gradient:#875CFF:#FF67D4><bold>OVERENCHANTED</bold></gradient> <white><enchantment> <level></white>'
      message-key: feedback.enchant.message
      subtitle: ''
      subtitle-key: feedback.enchant.subtitle
      duration-ms: 1800

      title:
        fade-in-ms: 150
        stay-ms: 900
        fade-out-ms: 250

      bossbar:
        color: PURPLE
        overlay: PROGRESS
        progress: 1.0

    sound:
      enabled: true
      key: minecraft:block.enchantment_table.use
      source: player
      volume: 0.85
      pitch: 1.20

    particles:
      enabled: true
      type: ENCHANT
      count: 35
      offset-x: 0.45
      offset-y: 0.65
      offset-z: 0.45
      speed: 0.08
      y-offset: 1.00
```

---

## Permissions

```text
overenchant.*
```

Grants access to every OverEnchant command.

```text
overenchant.use
```

Allows access to `/overenchant` and `/oe`.

```text
overenchant.enchant
```

Allows:

```text
/oe enchant
```

```text
overenchant.name
```

Allows:

```text
/oe name
```

```text
overenchant.lore
```

Allows all lore commands and lore shortcuts.

```text
overenchant.lang
```

Allows:

```text
/oe lang
```

```text
overenchant.reload
```

Allows:

```text
/oe reload
```

All OverEnchant permissions are `OP` by default.

Permission nodes can also be changed inside `config.yml`:

```yaml
permissions:
  use: overenchant.use
  enchant: overenchant.enchant
  name: overenchant.name
  lore: overenchant.lore
  lang: overenchant.lang
  reload: overenchant.reload
```

---

## Reloading

Reload OverEnchant with:

```text
/oe reload
```

This reloads the plugin configuration and the selected language file.

You do not need to restart the server every time you edit the configuration.

---

## Installation

1. Download `OverEnchant.jar`.
2. Put it inside your server's `plugins` folder.
3. Start or restart the server.
4. Configure `plugins/OverEnchant/config.yml` if needed.
5. Edit the files inside `plugins/OverEnchant/languages/` if you want custom messages.
6. Use `/oe` in game.

OverEnchant uses a **single universal JAR** for every supported Minecraft version.

You do not need to download a different build for each server version.

---

## Compatibility

OverEnchant `1.0.0` uses a **single universal JAR**.

Supported Minecraft versions:

```text
1.20.1
1.21.11
26.1.2
26.2
26.3
```

Officially supported platforms:

```text
Paper
Folia
```

The same `OverEnchant.jar` is used on every supported version.

### Java Requirements

Your required Java version depends on the Minecraft/Paper version used by your server.

```text
Minecraft 1.20.1 - 1.21.11 → Java 21
Minecraft 26.1.2 - 26.3    → Java 25
```

### Tested Compatibility

The universal JAR has successfully passed startup checks on all listed target versions with:

```text
Plugin enabled successfully
No startup errors
Configuration reload working
Language switching working
```

---

## Help Footer

The in-game help menu ends with:

```text
Made By • PupillaViola.
```

---

## Support

If you find a bug or need help with OverEnchant, contact on discord:

```text
pupillaviolaa
```
