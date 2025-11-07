# 🎯 Early Warning Radar Script (EWRS) for DCS World

[![DCS Version](https://img.shields.io/badge/DCS-2.9%2B-blue)](https://www.digitalcombatsimulator.com/)
[![MIST Version](https://img.shields.io/badge/MIST-4.5.126-green)](https://github.com/mrSkortch/MissionScriptingTools)
[![Version](https://img.shields.io/badge/version-1.6.0-orange)](https://github.com/Bob7heBuilder/EWRS)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)

> **A dynamic, realistic radar warning system that provides Bearing, Range, and Altitude (BRA) information to player aircraft in DCS World missions.**

![EWRS Banner](https://via.placeholder.com/1200x300/1a1a2e/eee?text=Early+Warning+Radar+Script)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [What's New in v1.6.0](#-whats-new-in-v160)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Configuration Guide](#-configuration-guide)
- [F10 Radio Menu](#-f10-radio-menu)
- [Supported Aircraft](#-supported-aircraft)
- [Supported Radar Units](#-supported-radar-units)
- [Usage Examples](#-usage-examples)
- [Troubleshooting](#-troubleshooting)
- [Credits](#-credits)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

EWRS transforms your DCS missions by providing realistic radar warning capabilities. Using actual in-game radar systems, it detects and reports hostile aircraft positions to friendly players, taking into account terrain masking, radar cross-sections, and electronic warfare considerations.

Perfect for:
- **Large-scale multiplayer missions**
- **Training scenarios**
- **Realistic combat operations**
- **SEAD/DEAD missions**
- **CAP (Combat Air Patrol) operations**

---

## ✨ Key Features

### 🎮 Realistic Detection
- Uses actual DCS radar systems for target detection
- Terrain masking and low-altitude flying are effective
- Beaming tactics work as intended
- RCS (Radar Cross Section) is respected

### 🔄 Dynamic Network
- Automatically detects new radar units spawned during mission
- Perfect for missions with CTLD (Complete Troops and Logistics Deployment)
- Adapts to changing battlefield conditions

### 📊 Customizable Reporting
- **Imperial** (feet, knots, NM) or **Metric** (meters, km/h, km) units
- Reference from **pilot's aircraft** or **mission bullseye**
- Adjustable update intervals and display times
- Limit number of threats displayed

### 🎯 Advanced Features
- **Bogey Dope**: Request nearest threat on-demand
- **Picture Reports**: Automated or on-demand threat overview
- **Friendly Picture**: See positions of friendly aircraft
- **Coalition Support**: Works for both RED and BLUE coalitions
- **Per-Group Settings**: Each flight can customize their preferences

### 🛠️ Mission Designer Flexibility
- Enable/disable automated messages
- Restrict BRA to certain aircraft types
- Control reference point options
- Set display limits and intervals

---

## 🆕 What's New in v1.6.0

### 🚀 Major Updates by HeavenDCS (2025)

#### DCS 2.9+ Compatibility
- Full API compatibility with latest DCS version
- Updated all function calls and syntax
- Verified against MIST 4.5.126

#### 30+ New Aircraft Types
Modern fighters and attack aircraft now supported:
- **F-14A/B Tomcat** 🦅
- **F-16C Viper** ✈️
- **F/A-18C/E/F Hornet/Super Hornet** 🐝
- **F-15E Strike Eagle** 🦅
- **F-4E Phantom II** 👻
- **AV-8B Harrier II** ⚡
- **A-10C II** ⚡
- **JF-17 Thunder** 🌩️
- **AH-64D Apache** 🚁
- **Mirage F1 variants** 🇫🇷
- **Su-30/Su-34 Flanker/Fullback** 🇷🇺
- **Tornado GR4/IDS** 🌪️
- **And many more!**

#### Expanded Radar Coverage
- All modern SAM systems included
- **Naval radar units now active** (carriers, destroyers, frigates)
- Updated AWACS aircraft list

#### Quality Improvements
- Comprehensive code validation
- Enhanced error handling
- Performance optimizations
- Improved documentation

---

## 📦 Requirements

### Essential
- **DCS World 2.9+** - [Download](https://www.digitalcombatsimulator.com/)
- **MIST 4.5.126 or later** - [Get MIST](https://github.com/mrSkortch/MissionScriptingTools)

### Recommended
- Mission with radar-equipped units (EWR, SAM sites, AWACS, or ships)
- Player-controlled aircraft
- Mission bullseye set (optional, for bullseye reference mode)

---

## 🔧 Installation

### Step 1: Download MIST
```bash
# Download MIST 4.5.126+
https://github.com/mrSkortch/MissionScriptingTools/releases
```

### Step 2: Add to Mission
1. Open your mission in the **DCS Mission Editor**
2. Go to **Triggers** → **Mission Start**
3. Add **DO SCRIPT FILE** action
4. Load `mist_4_5_126.lua` (or newer)
5. Add another **DO SCRIPT FILE** action
6. Load `EWRS.lua`

### Step 3: Configure
Edit `EWRS.lua` script options (see [Configuration Guide](#-configuration-guide))

### Step 4: Test
1. Place radar units (EWR, SAM, AWACS, or ships) in the mission
2. Add player aircraft
3. Add hostile aircraft
4. Run mission and check F10 menu

---

## 🚀 Quick Start

### Minimal Setup

```lua
-- In EWRS.lua, these are the essential settings:

ewrs.enableBlueTeam = true          -- Enable for Blue coalition
ewrs.enableRedTeam = true           -- Enable for Red coalition
ewrs.messageUpdateInterval = 30     -- Update every 30 seconds
ewrs.messageDisplayTime = 25        -- Show messages for 25 seconds
```

### Mission Requirements
1. **Radar Units**: Place at least one radar unit from the supported list
2. **Player Aircraft**: Add client slots for players
3. **Hostile Aircraft**: Add enemy aircraft for detection
4. **Bullseye** (optional): Set mission bullseye for reference

That's it! EWRS will automatically detect valid radar units and start providing BRA information.

---

## ⚙️ Configuration Guide

### Basic Settings

```lua
----SCRIPT OPTIONS----

-- Message Timing
ewrs.messageUpdateInterval = 30     -- Seconds between automated updates
ewrs.messageDisplayTime = 25        -- Seconds to display messages

-- Reference Options
ewrs.restrictToOneReference = false -- Allow players to change reference
ewrs.defaultReference = "self"      -- "self" or "bulls" (bullseye)
ewrs.defaultMeasurements = "imperial" -- "imperial" or "metric"

-- Coalition Settings
ewrs.enableRedTeam = true           -- Enable EWRS for RED coalition
ewrs.enableBlueTeam = true          -- Enable EWRS for BLUE coalition

-- Display Options
ewrs.disableFightersBRA = false     -- Disable BRA for fighters
ewrs.disableMessageWhenNoThreats = true -- Hide "no threats" messages
ewrs.maxThreatDisplay = 5           -- Max threats in picture (0 = all)
```

### Advanced Settings

```lua
-- Detection Realism
ewrs.useImprovedDetectionLogic = true -- Realistic radar limitations

-- On-Demand Mode
ewrs.onDemand = false               -- Disable auto messages, use F10 only

-- Special Features
ewrs.allowBogeyDope = true          -- Allow nearest threat requests
ewrs.allowFriendlyPicture = true    -- Allow friendly aircraft picture
ewrs.maxFriendlyDisplay = 5         -- Max friendlies shown
```

### Adding Custom Radar Units

```lua
-- Add to ewrs.validSearchRadars table
ewrs.validSearchRadars = {
    "YOUR_RADAR_UNIT_TYPE",         -- Add custom unit type names
    "p-10 s125 sr",                 -- SA-3 example
    -- ... existing radars
}
```

### Custom Aircraft Categories

```lua
-- Modify aircraft behavior
ewrs.acCategories = {
    [ "F-16C_50" ] = ewrs.FIGHTER,  -- Gets BRA messages
    [ "A-10C_2" ]  = ewrs.ATTACK,   -- Can be filtered
    [ "AH-64D_BLK_II" ] = ewrs.HELO -- Helicopter category
}
```

---

## 📻 F10 Radio Menu

Players access EWRS features through the F10 radio menu:

```
F10 → EWRS
├── Request Bogey Dope           (nearest threat)
├── Request Picture              (all threats - on-demand mode)
├── Request Friendly Picture     (friendly positions)
├── Set GROUP's reference point
│   ├── Set to Bullseye
│   └── Set to Self
├── Set GROUP's measurement units
│   ├── Set to Imperial (feet, knts)
│   └── Set to Metric (meters, km/h)
└── Turn Picture Report On/Off
    ├── Message ON
    └── Message OFF
```

### Menu Availability
| Feature | Auto Mode | On-Demand Mode |
|---------|-----------|----------------|
| Bogey Dope | ✅ (if enabled) | ✅ |
| Request Picture | ❌ | ✅ |
| Friendly Picture | ✅ (if enabled) | ✅ |
| Reference Settings | ✅ | ✅ |
| Measurement Units | ✅ | ✅ |
| Message On/Off | ✅ | ❌ |

---

## ✈️ Supported Aircraft

### Fighters (ewrs.FIGHTER)
- F-14A/B Tomcat
- F-15C/E Strike Eagle
- F-16C Viper (all blocks)
- F-4E Phantom II
- F-86F Sabre
- F/A-18C Hornet
- F/A-18E/F Super Hornet
- JF-17 Thunder
- M-2000C Mirage 2000C
- Mirage F1 (CE/EE/BE)
- MiG-29 (A/G/K/S variants)
- Su-27/30/33/34 Flanker family
- Tornado GR4/IDS

### Attack Aircraft (ewrs.ATTACK)
- A-10A/C/C II Warthog
- AV-8B Harrier II
- Bf-109K-4
- C-101 (EB/CC)
- F-5E-3 Tiger II
- FW-190D9
- Hawk
- L-39 (C/ZA)
- MB-339A
- MiG-15bis/19P/21Bis
- P-51D/TF-51D Mustang
- Su-25/T/TM Frogfoot
- Yak-52

### Helicopters (ewrs.HELO)
- AH-64D Apache
- Ka-50/50-3 Black Shark
- Mi-8MT Hip
- Mi-24P/V Hind
- OH-58D Kiowa
- SA342 Gazelle (M/L/Mistral)
- UH-1H Huey
- UH-60A Black Hawk

> **Note**: Aircraft categories determine if they receive BRA messages when `ewrs.disableFightersBRA = true`

---

## 📡 Supported Radar Units

### Ground-Based SAM Systems
| System | Type | Range |
|--------|------|-------|
| SA-3 Goa | Medium-range SAM | Search radar |
| SA-6 Gainful | Mobile SAM | Search & track |
| SA-10 Grumble | Long-range SAM | Search radar |
| SA-11 Gadfly | Mobile SAM | Search radar + TELAR |
| SA-15 Gauntlet | Point defense | Tor 9A331 |
| SA-19 Grison | SPAAG | Tunguska |
| Hawk | Medium-range SAM | Search radar |
| Patriot | Long-range SAM | Search & track |
| Roland | Short-range SAM | Search radar |
| Rapier FSA | Point defense | Blindfire radar |

### Early Warning Radars
- **55G6 EWR** - Long-range detection
- **1L13 EWR** - Long-range detection
- **Dog Ear (P-40)** - Mobile EWR

### AWACS Aircraft
- **A-50 Mainstay** (Russia)
- **E-2D Hawkeye** (USA)
- **E-3A Sentry** (USA)
- **KJ-2000** (China)

### Naval Units (⚓ All Active in v1.6.0)
| Ship Class | Name | Type |
|------------|------|------|
| CG 1164 | Moskva | Cruiser |
| CG-60 | Normandy | Ticonderoga cruiser |
| CGN 1144.2 | Pyotr Velikiy | Battlecruiser |
| CV 1143.5 | Admiral Kuznetsov | Carrier |
| CVN-70 | Carl Vinson | Supercarrier |
| CVN-71 | Theodore Roosevelt | Supercarrier |
| CVN-72 | Abraham Lincoln | Supercarrier |
| CVN-73 | George Washington | Supercarrier |
| CVN-75 | Harry S. Truman | Supercarrier |
| FF 1135M | Rezky | Frigate |
| FFG 11540 | Neustrashimy | Frigate |
| FFG-7CL | Oliver Hazzard Perry | Frigate |
| FFL 1124.4 | Grisha | Light frigate |
| FSG 1241.1MP | Molniya | Corvette |

---

## 📖 Usage Examples

### Example 1: Picture Report
```
EWRS Picture Report for: Viper 1-1 -- Reference: self

TYPE            BRG         RNG         ALT                  SPD            HDG
MiG-29S         045      32.4 NM       25000 ft             450 Knts       180
Su-27           067      28.1 NM       18000 ft             520 Knts       215
MiG-21Bis       089      41.2 NM       15000 ft             380 Knts       190
```

### Example 2: Bogey Dope
```
EWRS Bogey Dope for: Eagle 2-2

TYPE            BRG         RNG         ALT                  SPD            HDG
Su-30           134      18.7 NM       22000 ft             485 Knts       045
```

### Example 3: Unknown Contact
```
TYPE            BRG         RNG         ALT                  SPD            HDG
???                      POSITION                          UNKNOWN
```
*Radar detected contact but lacks type/range information*

### Example 4: Friendly Picture
```
EWRS Friendly Picture for: Hornet 3-1

TYPE            BRG         RNG         ALT                  SPD            HDG
F-16C_50        315      12.3 NM       20000 ft             420 Knts       090
F/A-18C         002       8.5 NM       18000 ft             390 Knts       085
```

---

## 🐛 Troubleshooting

### No BRA Messages Appearing

**Check:**
1. ✅ MIST is loaded **before** EWRS
2. ✅ At least one radar unit exists and is active
3. ✅ Hostile aircraft are present
4. ✅ Coalition is enabled (`ewrs.enableBlueTeam` or `ewrs.enableRedTeam`)
5. ✅ Player is in a supported aircraft
6. ✅ Messages aren't turned off via F10 menu

**Debug:**
```lua
-- Add to end of EWRS.lua
env.info("EWRS: Blue EWR Units: " .. #ewrs.blueEwrUnits)
env.info("EWRS: Red EWR Units: " .. #ewrs.redEwrUnits)
env.info("EWRS: Active Players: " .. #ewrs.activePlayers)
```

### Radar Not Detecting Targets

**Causes:**
- Target is terrain-masked (realistic!)
- Target is too low (below radar horizon)
- Target is beaming effectively
- Radar unit is destroyed
- Target RCS is very low

**Solutions:**
- Check radar unit status
- Verify target altitude and position
- Test with high-altitude, non-maneuvering target

### Messages Duplicated in Group

**This is expected behavior.** Due to DCS limitations, each pilot in a multi-aircraft group receives all messages for their group. Each message includes the pilot's name to clarify who it's for.

### F10 Menu Not Appearing

**Check:**
1. ✅ Player is in a client aircraft (not AI)
2. ✅ Player has spawned into the aircraft
3. ✅ Aircraft is in `ewrs.acCategories` table
4. ✅ `ewrs.disableFightersBRA` isn't blocking your aircraft type

### Script Errors

**Check DCS logs:**
- `Saved Games/DCS/Logs/dcs.log`

Look for lines containing "EWRS" to find error messages.

---

## 👏 Credits

### Original Author
**Steggles (Bob7heBuilder)**
- Original EWRS concept and development
- GitHub: [Bob7heBuilder/EWRS](https://github.com/Bob7heBuilder/EWRS)

### Recent Enhancements (v1.6.0 - 2025)
**HeavenDCS**
- DCS 2.9+ API compatibility update
- Added 30+ modern aircraft types
- Expanded radar units list with modern systems
- Activated all naval radar units
- MIST 4.5.126 compatibility verification
- Comprehensive testing and validation
- Enhanced documentation

### Special Thanks
- **MIST Development Team** - For the essential scripting framework
- **DCS Community** - For testing and feedback
- **ciribob & Stonehouse** - For group ID solutions
- **Rivvern** - For suggestions on threat display

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Reporting Issues
1. Check existing issues first
2. Provide detailed description
3. Include DCS version and MIST version
4. Attach relevant logs if possible
5. Describe steps to reproduce

### Suggesting Features
- Open an issue with `[Feature Request]` tag
- Explain use case and benefits
- Provide examples if possible

### Code Contributions
1. Fork the repository
2. Create a feature branch
3. Test thoroughly in DCS
4. Submit pull request with clear description
5. Follow existing code style

### Adding Aircraft/Radar Units
Submit PR with:
- Unit type name (exact DCS name)
- Category classification
- Test mission results

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Steggles (Bob7heBuilder) & HeavenDCS

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🔗 Links

- **Original Repository**: [Bob7heBuilder/EWRS](https://github.com/Bob7heBuilder/EWRS)
- **MIST Framework**: [MissionScriptingTools](https://github.com/mrSkortch/MissionScriptingTools)
- **DCS World**: [Digital Combat Simulator](https://www.digitalcombatsimulator.com/)

---

## 📊 Version History

| Version | Date | Key Changes |
|---------|------|-------------|
| 1.6.0 | 2025-01-07 | DCS 2.9+ compatibility, 30+ new aircraft, naval units active |
| 1.5.3 | Previous | Bug fixes, C-101CC added |
| 1.5.2 | Previous | F5E support |
| 1.5.1 | Previous | Gazelle added |
| 1.5.0 | Previous | Friendly picture feature |
| 1.4.1 | Previous | Ship radar support |
| 1.4.0 | Previous | Bogey dope, threat limits |
| 1.3.0 | Previous | On-demand picture reports |

---

<div align="center">

### ⭐ If you find EWRS useful, please give it a star! ⭐

**Made with ❤️ for the DCS Community**

[⬆ Back to Top](#-early-warning-radar-script-ewrs-for-dcs-world)

</div>
