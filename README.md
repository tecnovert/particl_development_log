# Particl Development Log


## 2021-02-12

Use Shuffle in random.h instead of std::shuffle to avoid self assign bug.

Found intermittent failure in rpc_part_filtertransactions
Amount search '70000' fails with an extra result.
Due to the anon output being randomly split. eg for a split of  -17.00000000 and -3.00000000 the filter will match the -17.


Various ci fixes.

- Fix is_PE_dll_32bit()
    - i386:x86-64 is 64bit

- Heap use after free in PlaceRealOutputs
    - CStoredTransaction stx was destroyed when it went out of scope.

- initialization-order-fiasco
    - Define another UNIX_EPOCH_TIME in insight module

    
## 2021-02-11

Extended RPC functions to allow anon transactions to be manually crafted.
Anon inputs must exist in the chain before being used, as the pubkey index is used in transactions.
Added inputs to coincontrol options on fundrawtransactionfrom to submit data for inputs not already part of the txn.


## 2021-02-08

- Wallet tracks anon watchonly transactions.
    - Incoming stealth watchonly pubkeys are added to mapWatchKeys in LegacyScriptPubKeyMan in addition to the script added to setWatchOnly.  Adding the pubkey is wasteful of memory, especially as it loads related scripts, but is the option most compatible with the rest of the code.  For tracking anon watchonly transactions checking if the destination script for the keyid is in setWatchOnly (if HaveWatchOnly()) in CWallet::IsMine(const CKeyID &address) would be enough.
    
Merged latest Bitcoin code into Particl:
- New AddCommand method on argsman.


## 2021-02-02

Merged latest Bitcoin code into Particl:
- avoid_reuse
    - Before the first received reused output would fall into the trusted balance category.
    - Now all reused outputs are marked reused

- validation.cpp
  - More functions moved to BlockManager class
  - Started a new particl namespace to contain Particl specific code and hopefully ease future merges as git has been mixing up the functions when automerging.

Pushed latest code to github.com/particl/coldstakepool

