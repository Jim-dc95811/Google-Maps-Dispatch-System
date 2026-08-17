# Map Fountain / Map Tank continuity checkpoint — superseded 2026-08-17

This file originally recorded the pre-arrival Map Tank design state on 2026-08-16. The physical tests completed on 2026-08-17 and changed the architecture decisively.

## Current truth

**The field appliance is router only.**

```text
native TPKX on USB SSD
→ GL.iNet Flint 2
→ Samba / SMB
→ Ethernet or Wi-Fi
→ Windows
→ ArcGIS Earth
```

The router provides local networking, DHCP, USB storage access, and file sharing. ArcGIS Earth supplies the GIS intelligence.

Do not reintroduce a field GIS-server appliance from older design history unless a new real-target failure proves that additional software is required.

## Live proof — 2026-08-17

Large specimen:

- `ESG1N.tpkx`
- 26,174,899,216 bytes by benchmark script
- 25,561,426 KB Windows File Explorer identification

### Ethernet benchmark — PASS

- random: 25.33 MiB/s
- random p95: 9.98 ms
- four-client aggregate: 51.21 MiB/s
- sequential: 42.58 MiB/s

### Wi-Fi benchmark — PASS

- random: 5.19 MiB/s
- random p95: 50.56 ms
- four-client aggregate: 5.31 MiB/s
- sequential: 6.14 MiB/s

The 536,870,912-byte Wi-Fi sequential sample completed in 83.440 seconds.

### ArcGIS Earth — PASS / LIVE-PROVEN

ArcGIS Earth opened `ESG1N.tpkx` directly from the Flint 2 Samba share over Wi-Fi and rendered/navigated the Jacksonville map while the file remained on the router-attached SSD.

That is the current architecture authority.

## Evidence hashes

```text
Ethernet benchmark screenshot
710e19a0676ada1729a35e13693b8ae81d0527fc3ba654a2da32288ac58244af

Ethernet PCAP
3eda0dc91dee83ac12a96912d8f7264e846c7393c3983de34970b5571a622f0f

Wi-Fi benchmark screenshot
631af7d06f433964175e1c3dc414767cc4c08f98af006406d8068be3b081ba3f

Wi-Fi PCAP
67db0a4dfee9519f933f0fc2e550da69634b293c815cd4b2d81413b38c60f1d4

ArcGIS Earth Wi-Fi success screenshot
8592abb26f9025baf665e4c4174670ba3a2bb433db96cbd092dd27355a9fd840
```

## Current branches

1. **Offline GeoStack** — master operational ArcGIS Earth field system, TPKX manufacturing, GNSS, PRAVE/F22/QR integration.
2. **Rasta Pyramid Factory** — high-resolution raster manufacturing to MBTiles, TPKX, or both.
3. **Map Fountain** — router-attached offline storage and local map delivery.

## Next gates

1. ArcGIS Earth direct-network comparison over Ethernet.
2. Real ArcGIS Earth navigation characterization over Wi-Fi.
3. Cold close/reopen and Wi-Fi reconnect.
4. Multiple simultaneous Eaters.
5. Simplest router-only ArcGIS Earth Mobile path.
6. Basecamp Feeder after consumption behavior is stable.

## Restart sentence

> Open the current Map Fountain README and acceptance record. The router-only USB-SSD → Samba → ArcGIS Earth path is LIVE-PROVEN over Wi-Fi. Continue from the next controlled gate; do not revive abandoned field-server architecture.
