.. index:: moused
.. _moused:

moused
******

This class handles all the settings for the moused daemon on the system
and provides per-device input device management.
:numref:`Table %s <mdreq>` shows the parameters for moused requests:

.. _mdreq:

.. table:: : Moused class request parameters

   +---------------+-----------+----------------------------------------+
   | Parameter     | Value     | Description                            |
   |               |           |                                        |
   +===============+===========+========================================+
   | id            |           | Any unique value for the request,      |
   |               |           | including a hash, checksum, or uuid.   |
   +---------------+-----------+----------------------------------------+
   | name          | moused    |                                        |
   |               |           |                                        |
   +---------------+-----------+----------------------------------------+
   | namespace     | sysadm    |                                        |
   |               |           |                                        |
   +---------------+-----------+----------------------------------------+
   | action        |           | "list_devices", "list_devices_active", |
   |               |           | "list_device_options",                 |
   |               |           | "read_device_options",                 |
   |               |           | "set_device_active",                   |
   |               |           | "set_device_inactive",                 |
   |               |           | "set_device_options"                   |
   +---------------+-----------+----------------------------------------+

The rest of this section provides examples of the available *actions*
for each type of request, along with their responses.

.. index:: moused list_devices
.. _moused list devices:

List Devices
============

The :command:`list_devices` action lists all detected devices on the
system with additionally relevant information.

**REST Request**

.. code-block:: none

 {
    "action" : "list_devices"
 }

**WebSocket Request**

.. code-block:: json

 {
    "id" : "fooid",
    "namespace" : "sysadm",
    "name" : "moused",
    "args" : {
       "action" : "list_devices"
    }
 }

**Response**

.. code-block:: json

 {
   "args": {
     "list_devices": {
       "psm0": {
         "description": "PS/2 Mouse",
         "device": "psm0",
         "driver": "psm",
         "parent": "atkbdc0"
       },
       "ums0": {
         "description": "YSTEK G Mouse, class 0/0, rev 1.10/0.01, addr 1",
         "device": "ums0",
         "driver": "ums",
         "parent": "uhub1",
         "active": "<"true" OR "false">"
       }
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: moused list_devices_active
.. _list devices active:

List Active Devices
===================

The :command:`list_devices_active` action lists all devices that are
currently active.

**REST Request**

.. code-block:: none

 PUT /sysadm/moused
 {
    "action" : "list_devices_active"
 }

**WebSocket Request**

.. code-block:: json

 {
    "name" : "moused",
    "namespace" : "sysadm",
    "id" : "fooid",
    "args" : {
       "action" : "list_devices_active"
    }
 }

**Response**

.. code-block:: json

 {
   "args": {
     "list_devices_active": {
       "active_devices": [
         "ums0"
       ]
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: moused list_device_options
.. _list device options:

List Device Options
===================

:command:`list_device_options` lists all the per-device options which
can be changed, with lists of possible settings or a description of the
possible settings types.

**REST Request**

.. code-block:: none

 PUT /sysadm/moused
 {
    "action" : "list_device_options"
 }

**WebSocket Request**

.. code-block:: json

 {
    "namespace" : "sysadm",
    "name" : "moused",
    "args" : {
       "action" : "list_device_options"
    },
    "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "list_device_options": {
       "accel_exponential": "float min=1.0 max=2.0",
       "accel_linear": "float min=0.01 max=100.00",
       "emulate_button_3": [
         "true",
         "false"
       ],
       "hand_mode": [
         "left",
         "right"
       ],
       "resolution": [
         "low",
         "medium-low",
         "medium-high",
         "high"
       ],
       "terminate_drift_threshold_pixels": "int min=0 max=1000",
       "virtual_scrolling": [
         "true",
         "false"
       ]
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: moused read_device_options
.. _read device options:

Read Device Options
===================

The :command:`read_device_options` action lists all the current settings
for a given device. There is one required argument:
:samp:`"device":"<device_id>"`.

**REST Request**

.. code-block:: none

 PUT /sysadm/moused
 {
    "device" : "psm0",
    "action" : "read_device_options"
 }

**WebSocket Request**

.. code-block:: json

 {
    "name" : "moused",
    "id" : "fooid",
    "namespace" : "sysadm",
    "args" : {
       "action" : "read_device_options",
       "device" : "psm0"
    }
 }

**Response**

.. code-block:: json

 {
   "args": {
     "read_device_options": {
       "accel_exponential": "1.0",
       "accel_linear": "1.0",
       "device": "psm0",
       "emulate_button_3": "false",
       "hand_mode": "right",
       "resolution": "medium-low",
       "terminate_drift_threshold_pixels": "0",
       "virtual_scrolling": "false"
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: moused set_device_active
.. _Set Device Active:

Set Device Active
=================

The :command:`set_device_active` action enables a device for use. The
:samp:`"device":"<device_id>"` argument is required.

**REST Request**

.. code-block:: none

 PUT /sysadm/moused
 {
    "device" : "ums0",
    "action" : "set_device_active"
 }

**WebSocket Request**

.. code-block:: json

 {
    "args" : {
       "device" : "ums0",
       "action" : "set_device_active"
    },
    "namespace" : "sysadm",
    "name" : "moused",
    "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "set_device_active": {
       "started": "ums0"
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: moused set_device_inactive
.. _set device inactive:

Set Device Inactive
===================

The :command:`set_device_inactive` action turns a specified mouse device
off. The argument :samp:`"device":"<device id>"` is required.

**REST Request**

.. code-block:: none

 PUT /sysadm/moused
 {
    "device" : "ums0",
    "action" : "set_device_inactive"
 }

**WebSocket Request**

.. code-block:: json

 {
    "namespace" : "sysadm",
    "args" : {
       "action" : "set_device_inactive",
       "device" : "ums0"
    },
    "name" : "moused",
    "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "set_device_inactive": {
       "stopped": "ums0"
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: moused set_device_options
.. _set device options:

Set Device Options
==================

The :command:`set_device_options` action changes the options for a
particular device. The argument :samp:`"device":"<device_id>"` is
required, with at least one of the available options for device
configuration. Including multiple options in a single API request is
allowed as well.

**REST Request**

.. code-block:: none

 PUT /sysadm/moused
 {
    "accel_exponential" : "1.5",
    "action" : "set_device_options",
    "device" : "psm0"
 }

**WebSocket Request**

.. code-block:: json

 {
    "id" : "fooid",
    "namespace" : "sysadm",
    "name" : "moused",
    "args" : {
       "accel_exponential" : "1.5",
       "device" : "psm0",
       "action" : "set_device_options"
    }
 }

**Response**

.. code-block:: json

 {
   "args": {
     "set_device_options": {
       "accel_exponential": "1.5",
       "accel_linear": "1.0",
       "device": "psm0",
       "emulate_button_3": "false",
       "hand_mode": "right",
       "resolution": "medium-low",
       "terminate_drift_threshold_pixels": "0",
       "virtual_scrolling": "false"
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

