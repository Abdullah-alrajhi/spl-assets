# SPL Assets — Phase 1 content seed

Optimized, transparent PNGs for the Saudi Pro League app (18 teams, 11 sample players).
All images are RGBA with transparent backgrounds and a white "die-cut" sticker keyline,
on the pure-black theme. Originals (~47 MB) were reduced to ~2.3 MB.

## Structure
```
teams/
  logos/{team-slug}.png      e.g. teams/logos/al-hilal.png        (≤512 px, ~28–94 KB)
players/
  headshots/{player-id}.png  e.g. players/headshots/1.png          (≤512 px, ~70–91 KB)
  icons/{player-id}.png      e.g. players/icons/1.png              (≤256 px, ~16–24 KB)
manifest.json                full mapping of ids ↔ slugs ↔ names ↔ paths
```

## URL pattern
Prepend your CDN base URL to any relative path in `manifest.json`:
```
{BASE}/teams/logos/al-hilal.png
{BASE}/players/headshots/1.png
{BASE}/players/icons/1.png
```

## Naming
- Teams: kebab-case slug of the English name (al-hilal, al-nassr, neom-sc, damac …).
- Players: numeric id (1–11), matching `spl_players.csv`. headshot id == icon id == same player.

## Processing applied
- Stripped macOS junk + all metadata.
- Logos & headshots: background removed (border-connected white only; interior whites kept),
  defringed, despeckled, and given a synthetic white keyline to match the icon sticker style.
- Icons: original transparency preserved untouched; only trimmed to content + resized.
- pngquant (alpha-safe lossy) + oxipng (lossless) compression.

## Note on fidelity
Logos & headshots were delivered flattened on white, so their keyline is reconstructed.
For maximum fidelity you can later re-export those from source WITH transparency and drop
them in at the identical filenames/paths — nothing else needs to change.
