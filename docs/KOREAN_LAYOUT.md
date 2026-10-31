# Supplied Korean image: verified layout evidence

The ISO filename labels this image Korean; the header alone does not verify its provenance.
Its DOL SHA-1 is `f08690e231921475b16619070c134c89f140042d`.
It shares the standard US executable's section addresses, section sizes, and named-function layout, but not all code or data bytes.
The included `marioUS.MAP` has stale read-only-data addresses.

Compared with standard US, the supplied image changes two English disc-error strings in `System/Application.cpp` from a trademark byte to `(TM)` and changes line wrapping.
Their new null-terminated lengths are 124 and 109 bytes, versus 121 and 106.
The first replacement fits in its previous aligned slot; the second moves subsequent strings by four bytes.
Later read-only data moves by eight bytes after alignment, consuming trailing padding.
The following exact byte-range equalities were checked before changing the configuration:

| US address range (end exclusive) | Korean address range | Evidence |
|---|---|---|
| `0x803734A0–0x803A4084` | same addresses | All bytes equal |
| `0x803A4124–0x803A4308` | `0x803A4128–0x803A430C` | All bytes equal |
| `0x803A4308–0x803AB658` | `0x803A4310–0x803AB660` | All bytes equal |

The two string symbols' sizes, subsequent `.rodata` symbol addresses, and translation-unit split boundaries were updated accordingly.
No C/C++ source was edited.
The corrected configuration rebuilds a DOL with the exact SHA-1 above.
The original-object split and named-function addresses were validated before computing overlap.
The original ISO and extracted linker map remain unchanged locally.

## Comparison against standard US

12,766 of 12,903 measured functions have exactly identical linked bytes, covering 96.9824% of measured function bytes.
Including relocation-masked candidates, 99.9062% have identical non-relocation instruction bytes.
This does not establish equal referenced data or behavior.
The following functions still differ outside relocation fields or in size:

| Function | Address | Size |
|---|---|---:|
| `drawDVDErr__12TApplicationFv` | `0x802A5B44` | 1036 |
| `initialize_nlogoAfter__12TApplicationFv` | `0x802A6A84` | 844 |
| `initialize_bootAfter__12TApplicationFv` | `0x802A6DD0` | 688 |
| `setupThreadFuncLogo__12TApplicationFv` | `0x802A70A0` | 804 |

The per-function comparison is preserved in `assets/comparison-vs-us.json`.
No equivalence is inferred for these changed functions.
