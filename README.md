# bip32
BIP 32 / BIP 44 tools for ETH and BTC

Usage:

```pycon
>>> import bip32

# Private master key from mnemonic or entropy
>>> master = bip32.HDKey.from_mnemonic('zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo when')
>>> master = bip32.HDKey.from_entropy(...bytes...)

# ETH
>>> master.derive_path("m/44'/60'/0'/0/0").eth_address
'bb2ca357e5780141f34500d43e492bee15531211'  # no leading "0x"

# BTC
>>> master.derive_path("m/44'/0'/0'/0/0").btc_address
'18bkaWvgTST8vJb2LgdBueo6sP4eoF99Ve'

# Unified address API (based on BIP 44)
>>> master.derive_path("m/44'/0'/0'/0/0").bip44_address
'bb2ca357e5780141f34500d43e492bee15531211'
>>> master.derive_path("m/44'/60'/0'/0/0").bip44_address
'18bkaWvgTST8vJb2LgdBueo6sP4eoF99Ve'

# Alternative representation of BIP 32 paths:
>>> master.derive_path([bip32.hardened(44), bip32.hardened(60), bip32.hardened(0), 0, 0])

# Raw public and private keys:
>>> master.derive_path("m/44'/60'/0'/0/0").public_key_bytes
b'\x02\xee\xd2\xa1r\xed,%\xff\xa7M\x10\xdbk7\x98{P\x8cq)\x112\x97\xcb\xa1\xbetf\x19\x12\x11\xb1'
>>> master.derive_path("m/44'/60'/0'/0/0").private_key_bytes
b'\x17\xb9SY\xef*3/\xa9\x17P{\\\xaf\xa0l9\x98\xd0E\x1cy\x16\xfd\xed\x9c\x92:\x7f\x8b\x86k'
```