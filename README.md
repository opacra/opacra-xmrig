# XMRig for Opacra

[XMRig](https://github.com/xmrig/xmrig) 6.26.0 with Opacra's mining algorithm, **RandomOPCA**
(`rx/opca`): RandomX with Opacra's own salt. Stock XMRig can't mine Opacra.

The launcher in the main Opacra download already mines; this build is for pools and for getting
the most from a fast processor. Website: [opacra.org](https://opacra.org).

## Download

From the [releases](https://github.com/opacra/opacra-xmrig/releases): Windows (`.zip`) and Linux
(`.tar.gz`), x86-64. Check the file before you run it:

| File | SHA-256 |
|---|---|
| `opacra-xmrig-6.26.0-opacra-1.0.0-win-x64.zip` | `9e900765326ff9a9f17ab6d8e46ee9d93ce37e4f6d50a5601e21d8cfb553934b` |
| `opacra-xmrig-6.26.0-opacra-1.0.0-linux-x64.tar.gz` | `810eaaa8364bb4743145a1ced64f95f00fcfae516262d1d4e721e5f5b6129960` |

`SHA256SUMS-xmrig-v1.0.0.asc` in the release holds both hashes, signed with the Opacra release key
(fingerprint `D861 7219 6FEC AAB6 84F5 B3FD CB65 D212 D0B1 162B`), the same key as the main
downloads. Antivirus programs often flag any mining program; the hash tells you the file is ours.

## Use

```
# with a pool (it gives you its address and port)
./xmrig -o POOL:PORT -a rx/opca -u YOUR_OPACRA_ADDRESS -p rig1 -k

# solo, against your own node (mainnet RPC port 29961, testnet 29971)
./xmrig -o 127.0.0.1:29961 --daemon -a rx/opca -u YOUR_OPACRA_ADDRESS
```

## Source

This build is XMRig v6.26.0 with `opacra-xmrig.patch`, which:

1. adds the algorithm `rx/opca` (RandomX with Opacra's salt; nothing else changed) and the coin
   `opacra` / `OPCA`;
2. lets solo (`--daemon`) mode accept Opacra block templates, whose coinbase has two outputs
   (the miner's and the 5% development fund).

Hashing, block submission and everything else are unchanged. `build-xmrig.sh` builds both
binaries (Linux natively, Windows with MinGW-w64) and sets XMRig's donation level to 0.

```
git clone https://github.com/xmrig/xmrig && cd xmrig && git checkout v6.26.0
git apply /path/to/opacra-xmrig.patch
mkdir build && cd build && cmake .. && make -j$(nproc)
```

## Licence

XMRig is free software under the GNU General Public License v3.0 (see `LICENSE`); so is this
build and the patch. No developer fee: the build sets XMRig's donation level to 0.
