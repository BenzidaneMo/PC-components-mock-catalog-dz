# PC components mock catalog (Algeria, 2026)

A ready-to-use demo catalog for e-commerce projects that sell PC parts: **245 products**
with realistic specs and prices, a category tree with typed spec definitions, 63 brands and
**160 product photos** (WebP). Every text a customer reads is available in **French, English and Arabic**.

It was extracted from the Rig.dz online shop project, where it seeds the database
(storefront, filters, comparison, PC builder with compatibility checks and PSU calculator).

## Contents

```
data/products.json     245 products
data/categories.json   category tree + spec definitions (labels fr/en/ar, units, enum options)
data/brands.json       63 brands (slug, name, website)
data/lookups.json      CPU sockets, memory types, form factors (used by compatibility fields)
images/products/       160 photos for 147 products (WebP, max 1000 px)
CREDITS.md             where prices, specs and photos come from
LICENSE-DATA.md        terms of use
```

## Conventions

- **Prices** are integers in Algerian dinars (DZD), no decimals. `salePrice` is `null` unless the product is on sale.
- **Translated text** is an object `{ "fr": …, "en": …, "ar": … }` (French is the reference). Product names are
  kept as sold (brand + model), untranslated.
- **Ids** are URL slugs (`amd-ryzen-5-5600`); `brand` and `category` reference `brands.json` / `categories.json` slugs.
- **Specs** are a flat object; the allowed keys, types, units and enum values of each category are in
  `categories.json` (a subcategory also inherits its parents' specs). Enum values are stable codes
  (`"nvme_pcie4"`), their labels are in the definition's `options`.
- **Images** are paths relative to this folder.

## Product fields

| Field | Type | Notes |
| --- | --- | --- |
| `id` | string | slug, unique |
| `sku` | string | `RIG-<PREFIX>-<nnn>` per category |
| `name` | string | |
| `brand`, `category` | string | slugs |
| `categoryPath` | string[] | root → leaf category slugs |
| `description` | {fr,en,ar} \| null | one line generated from the specs |
| `price`, `salePrice` | integer \| null | DZD |
| `currency` | "DZD" | |
| `stock` | integer | demo stock level |
| `status` | "active" | |
| `condition` | "new" \| "used" \| "refurbished" | `conditionNote` explains a used / refurbished item |
| `warrantyMonths`, `warrantyDays` | integer | |
| `buildOnly` | true | optional: sold only as part of a complete PC build |
| `socket` | string | CPU socket (CPUs) — see `lookups.json` |
| `memoryType` | string | RAM modules |
| `formFactor` | string | motherboards |
| `supports` | object | compatibility lists: `sockets`, `memoryTypes`, `formFactors` (boards, coolers, cases) |
| `specs` | object | see below |
| `parts`, `partIds` | array | prebuilt PCs: the components (names / ids of other products) |
| `images` | string[] | may be empty |
| `priceSource` | "licb+" \| "click-dz" \| "estimate" | see CREDITS.md |
| `imageSource` | {kind, page?} | "official" \| "retailer" \| "contributed" — see CREDITS.md |

### Spec keys per category

| Category | Keys |
| --- | --- |
| `processeurs` | `cores`, `threads`, `base_clock_ghz`, `boost_clock_ghz`, `l3_cache_mb`, `tdp_w`, `max_power_w`, `integrated_graphics`, `cooler_included`, `packaging` |
| `cartes-meres` | `chipset`, `memory_slots`, `max_memory_gb`, `m2_slots`, `pcie_gen`, `wifi` |
| `memoire-ram` | `capacity_gb`, `modules`, `speed_mts`, `cas_latency`, `rgb` |
| `cartes-graphiques` | `gpu_vendor`, `gpu_model`, `vram_gb`, `vram_type`, `tdp_w`, `recommended_psu_w`, `length_mm` |
| `stockage` | `capacity_gb`, `interface`, `drive_form_factor` |
| `ssd` | `read_mbs`, `write_mbs`, `dram_cache` |
| `disques-durs` | `rpm`, `cache_mb` |
| `alimentations` | `wattage_w`, `efficiency`, `modular`, `atx3` |
| `boitiers` | `case_type`, `max_gpu_length_mm`, `max_cooler_height_mm`, `max_radiator_mm`, `fans_included`, `side_panel` |
| `refroidissement` | `max_tdp_w`, `rgb` |
| `ventirads` | `height_mm`, `fan_size_mm` |
| `watercooling` | `radiator_mm` |
| `pates-thermiques` | `weight_g` |
| `ventilateurs` | `fan_size_mm` |
| `pc-gamer` | `cpu_model`, `gpu_model`, `ram_gb`, `storage_gb`, `storage_type`, `dedicated_gpu`, `os` |
| `pc-portables` | `cpu_model`, `gpu_model`, `ram_gb`, `storage_gb`, `storage_type`, `dedicated_gpu`, `os`, `size_inch`, `resolution`, `refresh_hz`, `layout`, `weight_kg` |
| `ecrans` | `size_inch`, `resolution`, `refresh_hz`, `panel`, `response_ms`, `curved` |
| `claviers` | `layout`, `switch_type`, `size`, `wireless`, `rgb` |
| `souris` | `dpi`, `weight_g`, `wireless`, `rgb` |
| `casques` | `connection`, `microphone`, `surround` |
| `webcams` | `video`, `microphone` |
| `microphones` | `connection`, `pattern` |
| `imprimantes` | `print_technology`, `color`, `functions`, `wifi`, `duplex`, `speed_ppm` |
| `routeurs` | `wifi_standard`, `speed_mbps`, `lan_ports`, `mesh`, `sim_4g` |
| `adaptateurs-wifi` | `wifi_standard`, `bus`, `bluetooth` |
| `switchs` | `ports`, `port_speed`, `managed` |
| `cables-reseau` | `cable_category`, `length_m` |
| `tapis-de-souris` | `pad_size`, `rgb` |
| `chaises-gaming` | `max_load_kg`, `upholstery` |
| `tables-gaming` | `width_cm`, `depth_cm` |
| `manettes` | `platform`, `wireless` |
| `sacs` | `max_laptop_inch` |
| `cables-adaptateurs` | `cable_type`, `length_m` |

## Categories

- `composants` PC components
  - `processeurs` Processors (25)
  - `cartes-meres` Motherboards (20)
  - `memoire-ram` Memory (RAM) (12)
  - `cartes-graphiques` Graphics cards (16)
  - `stockage` Storage
    - `ssd` SSDs (18)
    - `disques-durs` Hard drives (4)
  - `alimentations` Power supplies (15)
  - `boitiers` Cases (19)
  - `refroidissement` Cooling
    - `ventirads` Air coolers (10)
    - `watercooling` AIO liquid coolers (9)
    - `pates-thermiques` Thermal paste (3)
    - `ventilateurs` Case fans (1)
- `pc-gamer` Prebuilt PCs
  - `pc-gamer-fixe` Gaming PCs (4)
  - `pc-bureau` Office PCs (2)
- `pc-portables` Laptops
  - `portables-gaming` Gaming laptops (5)
  - `portables-bureautique` Office laptops (3)
- `peripheriques` Peripherals
  - `ecrans` Monitors (11)
  - `claviers` Keyboards (9)
  - `souris` Mice (13)
  - `casques` Headsets (7)
  - `webcams` Webcams (3)
  - `microphones` Microphones (4)
  - `imprimantes` Printers (4)
- `reseau` Networking
  - `routeurs` Wi-Fi routers (4)
  - `adaptateurs-wifi` Wi-Fi adapters (2)
  - `switchs` Switches (2)
  - `cables-reseau` Network cables (2)
- `accessoires` Accessories & gaming gear
  - `tapis-de-souris` Mouse pads (4)
  - `chaises-gaming` Gaming chairs (4)
  - `tables-gaming` Gaming desks (1)
  - `manettes` Controllers (4)
  - `sacs` Bags & sleeves (2)
  - `cables-adaptateurs` Cables & adapters (3)

## Quick start (Node)

```js
const products = require("./data/products.json");
const gpus = products.filter((p) => p.category === "cartes-graphiques");
const cheapest = gpus.sort((a, b) => (a.salePrice ?? a.price) - (b.salePrice ?? b.price))[0];
console.log(cheapest.name, cheapest.price, "DA", cheapest.images[0]);
```

## Caveats

- Prices are a **snapshot of the Algerian market in 2026**; 156 of them are estimates (see CREDITS.md).
- Stock levels, SKUs, sales and the "Rig.dz" prebuilt PCs are invented for the demo.
- 98 products have no photo.
- The photos belong to their manufacturers / retailers: read CREDITS.md and LICENSE-DATA.md before using them
  anywhere public.
