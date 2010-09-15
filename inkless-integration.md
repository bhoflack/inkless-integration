Inkless integration
===================
------------
Introduction
------------

Inkless integration is a event driven system which consists out of a couple of services and a message bus.

----------
Processors
----------

ProbingWafermapProcessors
-------------------------
This processor gets probing wafermaps for a given lotname.

**in**
The message is a TextMessage containing an XML document.

For example

    <lot name="66666" />

**out**
A ByteMessage containing a list of byteArrays with the wafermaps.


ConvertWafermapToTH01Processor
------------------------------
This processor converts a wafermap from probing format to TH01 format.

**in**
The message is a ByteMessage containing the wafermap.

**out**
A ByteMessage containing the th01 wafermap.

ExtractPassCountProcessor
-------------------------
This processor extracts the pass count from a TH01 wafermap.

**in**
A ByteMessage containing a th01 wafermap.

**out**
A TextMessage containing an XML document

For example

    <lot name="66666" wafer="1" passcount="2345" />


--------
Adaptors
--------

TransactionAdaptor
------------------

The transactionAdaptor detects when a lot has been moved in Oracle,  and sends a message with the lotname.

**out**
A TextMessage containing an xml document.

For example

    <lot name="66666" />


CollectionPlanAdaptor
---------------------

The collection plan adaptor fills in the collection plan for a particular transaction in Oracle.

**in**
A TextMessage containing an xml document.

For example

    <lot name="66666">
      <wafer id="1" passcount="12345" />
      <wafer id="2" passcount="4567" />
      <wafer id="3" passcount="9875" />
    </lot>
