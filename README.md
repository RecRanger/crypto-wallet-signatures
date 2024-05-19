# crypto-wallet-signatures

Notes about raw signatures and storage types of various crypto wallet formats

This inventory is intended to aid data recovery tool creation, and give a starting point for those doing research on wallet formats.

## Bitcoin Core/QT/Bitkeys Wallet Format

* Storage Type: Berkeley DB
* Default Name: `wallet.dat`
* Path: `~/.bitcoin/wallet.dat` or `C:\Users\YourUserName\AppData\Roaming\Bitcoin\wallet.dat`
* Magic Bytes: Berkeley DB (Btree, version 9, native/little-endian byte-order)
  * Hex: `00 00 00 00 01 00 00 00 00 00 00 00 62 31 05 00`
* Strings in the file:
  * Hex: `01308201130201010420` -> pre-2012 non-encrypted wallet (searchable with keyhunter)
  * Hex: `01d63081d30201010420` -> post-2012 non-encrypted wallet (searchable with keyhunter)

## Armory Wallet

* Storage Type: proprietary binary format
* Example Name: `armory_21o7Xe3H5_.wallet` and `armory_21o7Xe3H5_.wallet.backup`
* Magic Bytes:
  * Short Version (hex): `ba 57 41 4c 4c 45 54 00`
  * Full Version (hex): `ba 57 41 4c 4c 45 54 00 60 fe cd 00 f9 be b4 d9`
* Contains checksums of varying lengths (including 16, 20, 32, 44, and 65-length checksums)
* Specification of format is published: https://www.bitcoinarmory.com/wallet-format/


## MultiBit Wallet Keys Export

* Example Name: `bitcoin-wallet-keys-2013-12-05`
* Storage Type: \< 500-byte base64-encoded encrypted string
* Strings in the file:
  * Starts with ASCII: `U2FsdGVkX18` -> "Salted__", when decoded from base64 to ASCII


## MultiBit Wallet
* Strings in the file:
  * `org.bitcoin.production`

## MultiDOGE Wallet
* Strings in the file:
  * `org.dogecoin.production`

## Electrum Wallet

* Includes Electrum, ElectronCash, and other forks
* Storage Type: JSON file, or Python repr in very early versions (<1.9)
* Default Name: `default_wallet`
* Path: `~/.electrum/wallets/default_wallet` or `C:\Users\YourUserName\AppData\Roaming\Electrum\wallets\default_wallet`
* Strings in the file:
  * All versions (including very far back): `seed_version`
* Modern versions don't list the addresses outright.

## Nomenclature

* All hex strings are in little-endian byte order; that is, if you read the file one-byte-at-a-time from left to right, you will read the bytes in the order they are written in the hex string.

## Contributing

Please feel free to submit a pull request with additional information about wallet formats, or to correct any errors in this document.

Please Star this repository if you find it useful.

## Related Projects

* https://github.com/RecRanger/etc_magic

