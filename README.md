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
