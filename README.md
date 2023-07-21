# Lightweight Beaconchain Explorer

<b>This is a work in progress project!\
It's not ready to be used in any way yet.</b>

## What is this?
This project is planned to become a lightweight beaconchain explorer.

A Beaconchain explorer is a tool that allows users to view and interact with the data on the Ethereum Beacon Chain. It is similar to a blockchain explorer, which allows users to view data on a blockchain such as the current state of transactions and blocks - but focussed on exploring the beaconchain.

This "lightweight" explorer is planned to proxy most of the queries to an underlying standard beacon node api, which makes it a lot easier and cheaper to run (no 3rd party proprietary database like bigtables required)

## Background
https://github.com/ethpandaops/tooling-wishlist/blob/master/tools/lightweight-beaconchain-explorer.md

## TODO

(More for myself to keep track of what is done / needs to be done)

* [ ] Explorer Pages (UI)
  * [ ] Layout polishing
  * [ ] Startpage
  * [ ] Epoch Overview (`/epochs`)
  * [ ] Slots Overview (`/slots`)
  * [x] Slot details (`/slot/{slot_or_root}`)
    * [x] Overview, Attestations, Slashings, Deposits, BLSChanges, Withdrawals, Voluntary Exits
    * [ ] Blob Sidecars
    * [ ] Enhance view controls (Hex/UTF8 Grafitti, Local/UTC Time, Copy Buttons etc.)
  * [ ] Search (Block Root, Epoch Number, Slot Number, Grafitti)
    * [ ] Type-Ahead search
* [ ] RPC Client / Caching
  * [x] Get Block Header by slot / block root
  * [x] Get Block Body by block root
  * [x] Get Epoch assignments (proposer, attester & sync committee duties)
    * [x] Simple cache for epoch duties
    * [ ] Persistent cache for epoch duties in DB
* [ ] Database
  * [ ] Schema initialization / upgrade
  * [x] Table: Blocks (Slot index for search & slot overview)
  * [x] Table: Epochs (Epoch index for startpage & epoch overview)
  * [x] Table: SyncState (keeps track of synchronization state for Blocks & Epochs indexes)
* [ ] Indexer
  * [x] Keep track of current & last epoch in memory
  * [x] Aggregate Votes
  * [x] Check for chain reorgs and track orphaned blocks
    * [x] Save orphaned blocks in db (header & body)
    * [ ] Handle large chain reorgs with >32 slots (needs re-indexing of affected epochs)
  * [x] Update Slot index in DB
  * [x] Update Epoch index in DB
  * [x] Synchronization (index older epochs)
