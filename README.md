# DMGE Tiles Library

The official open-source tile library for the **Dungeon Master Game Engine (DMGE)**.

Engineered for procedural map generation via **Wave Function Collapse (WFC)**, seamless offline caching, and automated line-of-sight raycasting.

---

## 📐 Tile Specification & Standards

Each tile definition in `manifest.json` conforms to the DMGE Tile Schema:

```json
{
  "id": "dungeon_wall_n",
  "name": "Dungeon Wall North",
  "biome": "dungeon",
  "category": "wall",
  "file": "dungeon/wall_n.svg",
  "sockets": {
    "north": "wall",
    "east": "wall_side_n",
    "south": "floor",
    "west": "wall_side_n"
  },
  "blockingSegments": [
    [0.0, 0.375, 1.0, 0.375]
  ],
  "castsShadow": true,
  "weight": 2.0,
  "tags": ["stone", "wall", "north"]
}
```

### 1. Sockets & WFC Adjacency
- Sockets (`north`, `east`, `south`, `west`) define boundary compatibility.
- Two adjacent tiles can be placed side-by-side if their connecting socket identifiers match.
- Core socket labels:
  - `floor`: Standard open walkable floor.
  - `wall`: Solid masonry or void exterior.
  - `wall_side_*`: Inter-wall alignment sockets.

### 2. Automated Line-of-Sight (`blockingSegments`)
- Coordinates are normalized (`0.0` to `1.0`) relative to tile dimensions: `[x1, y1, x2, y2]`.
- When WFC collapses tiles onto the canvas, DMGE automatically projects these segments into the PixiJS 8 raycasting engine, instantly creating walls for dynamic Fog of War without any manual DM drawing.

---

## 🚀 Usage in DMGE

DMGE pulls `manifest.json` and referenced assets on first launch, storing them in client-side IndexedDB for 100% offline gameplay.

## 📄 License

MIT License. Free to use in personal and commercial tabletop projects.
