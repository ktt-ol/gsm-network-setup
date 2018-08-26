Configuration files for GSM network with LimeSDR and Debian
using the legacy `osmo-nitb` setup and built-in call routing.
The configuration uses ARFCN128 from GSM850 band. You need a
license in most (all?) countries of the world. In Germany it
can be requested at Bundesnetzagentur.

## Install

 * `apt install osmocom-nitb osmo-bts osmo-trx`
 * `apt install libosmocore-dev liblimesuite-dev`
 * `git clone "https://git.osmocom.org/osmo-trx" ; cd osmo-trx ; ./autogen.sh ; ./configure --with-lms --without-uhd ; make ; cd ..`

## Run

1. Run `osmo-nitb -c open-bsc.cfg -l hlr.sqlite3 -P -C --debug=DRLL:DCC:DMM:DRR:DRSL:DNM`
2. Run `sudo ./osmo-trx/Transceiver52M/osmo-trx-lms` (root is required for realtime scheduling)
3. Run `osmo-bts-trx -c osmo-bts.cfg`

## Control Interface

 * OpenBSC `telnet 127.0.0.1 4242`
 * OpenBTS `telnet 127.0.0.1 4241`
 * OsmoTRX `telnet 127.0.0.1 4237`

## Usage

osmo-nitb will automatically add subscriber entries when a phone tries
connecting to the network. By default the subscriber will not be authorized
and thus will be rejected. The OpenBSC control interface can be used
to change the settings of the subscriber:

```
OpenBSC# subscriber id 6 authorized 1 
OpenBSC# subscriber id 6 extension 2342
OpenBSC# subscriber id 6 name test
OpenBSC# show subscriber id 6
    ID: 6, Authorized: 1
    Name: 'test'
    Extension: 2342
    LAC: 1337/0x539
    IMSI: 262423403002139
    TMSI: 038ED03C
    Expiration Time: Mon, 27 Aug 2018 00:16:58 +0200
    Paging: not paging Requests: 0
    Use count: 1
```
