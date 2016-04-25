# Bluz Node Gateway

run with node index.js.  currently logging is set pretty verbose.  Works on at least two DKs on the C.H.I.P.

## Some basic info about the Bluz- Particle bridging

First, enable notify (write [0x01,0x00] to CCCD descriptor)

* Cloud --> DK:
 * sends on `871e022538ff77b1ed419fb3aa142db2` characteristic
 * send a [0x01,0x00] header
 * send data in 20 byte chunks, max total length 960 bytes;
 * send a [0x03,0x04] end 
* DK -> Cloud
 * notification should have been enabled on read (`871e022438ff77b1ed419fb3aa142db2`) characteristic
 * have to buffer data, as DK can only send in 20 byte chunks
 * first chunk starts with the service type (0x01 is for cloud, 0x02 is the Particle ID data (see below))
 * after all chunks of the data to be sent are done, the DK will also end strings with a [0x03,0x04] 
 * 
* Also, a [0x02,0x00] data write with _no_ header will result in the next data from the DK being the Particle ID  