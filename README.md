# ESB-Docs
asyBiomeGenerator Plugin

**A Minecraft plugin that creates custom biome worlds and keeps them clean automatically!**

---

## 🎮 What Does This Plugin Do?

This plugin helps you create and maintain special Minecraft worlds with custom biomes. Think of it as a world manager that:

- Creates worlds filled with only one biome (desert, plains, mushroom, etc.)
- Automatically repairs broken blocks in your worlds
- Shows players countdown timers for when repairs happen
- Keeps your mining/PvP worlds fresh and clean

---

## ✨ Main Features

### 1. **Custom Biome Worlds**
Create entire worlds with just one biome type:
- 🏜️ **Desert** - Sandy worlds, perfect for building
- 🌾 **Plains** - Flat grass worlds
- 🍄 **Mushroom** - Unique mushroom cave worlds
- 🏔️ **Mesa** - Red clay worlds
- 🌌 **End** - End-style dimensions
- 🌴 **Jungle** - Tropical worlds

### 2. **Smart World Repair**
- Fixes only broken/griefed areas
- Keeps player builds intact
- Works WITHOUT restarting your server
- Perfect for mining worlds that get destroyed

### 3. **Auto-Repair Scheduling**
- Set worlds to repair automatically (every hour, daily, etc.)
- Players see countdown timers
- No manual work needed!

### 4. **Complete World Reset**
- Wipe entire worlds clean
- Start fresh anytime
- Instant reload (no restart)

---

## 📦 Installation

### Step 1: Download Required Plugins
1. **EasyBiomeGenerator** (this plugin)
2. **Multiverse-Core** - [Download here](https://dev.bukkit.org/projects/multiverse-core)
3. **PlaceholderAPI** (optional, for countdown timers) - [Download here](https://www.spigotmc.org/resources/placeholderapi.6245/)

### Step 2: Install
1. Stop your server
2. Put all 3 plugins in your `plugins/` folder
3. Start your server
4. **Set up bukkit.yml BEFORE creating worlds**: Configure `bukkit.yml` to ensure generator persistence. This step is crucial for keeping your custom biomes after server restarts.

---

## 🎯 Quick Start Guide

### Creating Your First Custom World

**1. Create a desert mining world:**
```
/mv create mining normal -g EasyBiomeGenerator:desert
```

**2. Teleport to it:**
```
/mv tp mining
```

**3. That's it!** You now have a world filled with desert biome.

### ⚠️ IMPORTANT: Making Generators Persist After Restart

After creating your world, you **MUST** add it to `bukkit.yml` or the custom biome will be lost when you restart your server!

**Step 1: Find bukkit.yml**
- Located in your server's main folder
- Same folder as `server.jar`

**Step 2: Open bukkit.yml and add your world**

Add this at the bottom of the file:
```yaml
worlds:
  mining:
    generator: EasyBiomeGenerator:desert
```

**Step 3: Save and restart**

**Complete Example (Multiple Worlds):**
```yaml
worlds:
  mining:
    generator: EasyBiomeGenerator:desert
  plains_world:
    generator: EasyBiomeGenerator:plains
  mushroom_cave:
    generator: EasyBiomeGenerator:mushroom
  pvp_arena:
    generator: EasyBiomeGenerator:mesa
```

**📌 Important Notes:**
- World names must match EXACTLY (case-sensitive)
- Use the same biome type you used when creating the world
- This prevents "generator lost" warnings
- Do this IMMEDIATELY after creating each world

**Quick Command to Check:**
```
/es config
```
This shows you EXACTLY what to add to bukkit.yml!

### Other Biome Examples

```
/mv create plains_world normal -g EasyBiomeGenerator:plains
/mv create mushroom_cave normal -g EasyBiomeGenerator:mushroom
/mv create mesa_world normal -g EasyBiomeGenerator:mesa
/mv create end_world normal -g EasyBiomeGenerator:end
```

---

## 🔧 Commands

### View Your Worlds
```
/es list
```
Shows all worlds managed by this plugin.

### Repair Broken Chunks
```
/es repair <worldname> confirm
```
**Example:** `/es repair mining confirm`

**What it does:**
- Scans for broken/griefed chunks
- Fixes only the damaged areas
- Keeps good chunks untouched
- Works instantly (no restart needed)

### Complete World Reset
```
/es reset <worldname> confirm
```
**Example:** `/es reset mining confirm`

**What it does:**
- Deletes EVERYTHING
- Regenerates the entire world
- Fresh start
- Works instantly

### Check World Status
```
/es diagnose <worldname>
```
Shows if the world is set up correctly.

### Get Help
```
/es help
```

---

## ⚙️ Setting Up Auto-Repair

### What is Auto-Repair?

Auto-repair automatically fixes your worlds at scheduled times. Perfect for:
- Mining worlds (repair every hour)
- PvP arenas (repair after battles)
- Resource worlds (daily reset)

### Configuration

Edit `plugins/EasyBiomeGenerator/config.yml`:

```yaml
auto-repair:
  enabled: true
  
  worlds:
    mining:
      enabled: true
      interval: 3600  # Repair every 1 hour
    
    pvp_arena:
      enabled: true
      interval: 7200  # Repair every 2 hours
    
    resource_world:
      enabled: true
      interval: 86400  # Repair once per day
```

### Time Intervals Cheat Sheet

| How Often | Seconds |
|-----------|---------|
| Every 15 minutes | 900 |
| Every 30 minutes | 1800 |
| Every hour | 3600 |
| Every 2 hours | 7200 |
| Every 6 hours | 21600 |
| Once per day | 86400 |

---

## 📊 Countdown Timers (PlaceholderAPI)

### What Are Countdown Timers?

Show players when the next repair happens! Works with scoreboards and holograms.

### Placeholder Format
```
%easyreset_resettime_<worldname>%
```

### Examples

**Show mining world countdown:**
```
%easyreset_resettime_mining%
```

**Show in scoreboard:**
```
&eMining World Resets In:
&f%easyreset_resettime_mining%
```

**Displays as:**
```
Mining World Resets In:
01:45:30
```

### Where to Use Placeholders?

- **Scoreboards** (FeatherBoard plugin)
- **Holograms** (HolographicDisplays plugin)
- **TAB** (TAB plugin)
- **Chat** (DeluxeChat plugin)
- **Signs** (Various sign plugins)

---

## 🎨 Example Setups

### Mining World (Hourly Repair)

**1. Create world:**
```
/mv create mining normal -g EasyBiomeGenerator:desert
```

**2. Configure auto-repair in config.yml:**
```yaml
mining:
  enabled: true
  interval: 3600  # 1 hour
```

**3. Add scoreboard (with FeatherBoard):**
```yaml
lines:
  - "&6&lMining World"
  - "&eResets in: &f%easyreset_resettime_mining%"
```

**Done!** Players mine, world repairs every hour automatically.

---

### PvP Arena (Quick 30-Minute Repair)

**1. Create arena:**
```
/mv create pvp_arena normal -g EasyBiomeGenerator:mesa
```

**2. Configure auto-repair:**
```yaml
pvp_arena:
  enabled: true
  interval: 1800  # 30 minutes
```

**3. Add hologram:**
```
/hd create arena_timer
/hd addline arena_timer &c&lPvP Arena
/hd addline arena_timer &fResets: &e%easyreset_resettime_pvp_arena%
```

---

## 🛠️ Common Use Cases

### 1. **Mining World**
- Players dig freely
- Auto-repairs every hour
- Never runs out of resources
- No manual reset needed

### 2. **PvP Arena**
- Battles destroy terrain
- Auto-repairs after fights
- Always clean for next battle

### 3. **Resource World**
- Players gather resources
- Resets daily
- Fresh resources every day

### 4. **Building World**
- Use `/es repair` to fix griefing
- Keeps good builds intact
- Only removes broken areas

---

## ❓ FAQ

### Q: Do I need to restart my server to repair worlds?
**A:** No! Repairs happen instantly while the server is running.

### Q: Will auto-repair delete player builds?
**A:** The **repair** command only removes broken/griefed chunks. Good builds stay intact. Use **reset** if you want to delete everything.

### Q: How do I stop auto-repair for a world?
**A:** Set `enabled: false` in config.yml for that world.

### Q: Can I repair worlds manually?
**A:** Yes! Use `/es repair <world> confirm` anytime.

### Q: What's the difference between repair and reset?

| Command | What It Does |
|---------|--------------|
| `/es repair` | Fixes only broken chunks, keeps builds |
| `/es reset` | Deletes everything, complete fresh start |

### Q: Do I need PlaceholderAPI?
**A:** Only if you want countdown timers. Auto-repair works without it.

### Q: Can I use this with Multiverse-Core?
**A:** Yes! In fact, it's required. They work perfectly together.

---

## 🎯 Permissions

| Permission | What It Does | Default |
|------------|--------------|---------|
| `easybiome.*` | All plugin commands | OP only |
| `easybiome.reset` | Use repair/reset commands | OP only |

**Note:** Regular players can see countdown timers, but only OPs can repair/reset worlds.

---

## 📝 Example Server Setup

Here's how a typical server uses this plugin:

**Worlds:**
- `lobby` - Normal world (no auto-repair)
- `mining` - Desert world, repairs every hour
- `pvp` - Mesa world, repairs every 30 minutes
- `resource` - Plains world, resets daily

**config.yml:**
```yaml
auto-repair:
  enabled: true
  worlds:
    mining:
      enabled: true
      interval: 3600
    pvp:
      enabled: true
      interval: 1800
    resource:
      enabled: true
      interval: 86400
```

**Scoreboard shows:**
```
─────────────────
   Server Info
─────────────────
Mining resets:
01:23:45

PvP resets:
00:15:30

Resource resets:
18:45:00
─────────────────
```

---

## 🔍 Troubleshooting

### ⚠️ World lost custom biome after restart (MOST COMMON ISSUE)

**Problem:** After restarting your server, your custom desert/plains/mushroom world turned into normal Minecraft terrain.

**Cause:** You didn't add the world to `bukkit.yml`

**Fix:**
1. Open `bukkit.yml` in your server's main folder
2. Add your world configuration:

```yaml
worlds:
  your_world_name:
    generator: EasyBiomeGenerator:biome_type
```

3. Replace `your_world_name` with your actual world name
4. Replace `biome_type` with the biome you used (desert, plains, mushroom, mesa, end)
5. Save the file
6. Restart server

**Quick way to check what to add:**
```
/es config
```
This command shows you the EXACT configuration to copy-paste!

**Example Complete bukkit.yml:**
```yaml
# This is what a properly configured bukkit.yml looks like
settings:
  allow-end: true
  warn-on-overload: true
  # ... other settings ...

worlds:
  mining:
    generator: EasyBiomeGenerator:desert
  pvp_arena:
    generator: EasyBiomeGenerator:mesa
  resource_world:
    generator: EasyBiomeGenerator:plains
```

### World doesn't have custom biome

**Fix:**
1. Check you used the right command format
2. Make sure generator is in bukkit.yml (see above)
3. Use `/es diagnose <world>` to check

### Repair doesn't work
**Fix:**
1. Make sure you used `confirm`: `/es repair world confirm`
2. Check console for errors
3. **Verify bukkit.yml configuration**: Ensure the world is added to `bukkit.yml` with the correct generator.

### Placeholder shows "Not scheduled"
**Fix:**
1. Add world to config.yml auto-repair section
2. Set `enabled: true`
3. Restart server
4. **Verify bukkit.yml configuration**: Ensure the world is added to `bukkit.yml` with the correct generator.

### Countdown not updating
**Fix:**
1. Install PlaceholderAPI
2. Restart server
3. Test: `/papi parse me %easyreset_resettime_world%`
4. **Verify bukkit.yml configuration**: Ensure the world is added to `bukkit.yml` with the correct generator.

---

## 📞 Support

Need help? Check these files:
- `AUTO_REPAIR_GUIDE.md` - Detailed auto-repair guide
- `GENERATOR_PERSISTENCE_GUIDE.md` - Technical setup guide

---

## 🎉 Quick Summary

✅ Create custom biome worlds  
✅ Auto-repair broken chunks  
✅ Schedule automatic repairs  
✅ Show countdown timers to players  
✅ No server restarts needed  
✅ Perfect for mining/PvP/resource worlds  

**It's that simple!** Create worlds, set auto-repair, and forget about manual maintenance. Your players will love always having fresh, clean worlds to play in! 🚀

---

**Version:** 2.0.0  
**Author:** KushDev  
**Requires:** Multiverse-Core  
**Optional:** PlaceholderAPI (for countdown timers)
