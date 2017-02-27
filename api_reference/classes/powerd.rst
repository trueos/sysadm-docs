.. index:: powerd
.. _powerd:

powerd
******

The powerd utility monitors the system state and sets various power
control options accordingly. It offers power-saving modes that can be
individually selected for operation on AC power or batteries.

:numref:`Table %s <pdreq>` shows the parameters for powerd requests:

.. _pdreq:

.. table:: : Powerd class request parameters

   +---------------+-----------+-----------------------------------------+
   | Parameter     | Value     | Description                             |
   |               |           |                                         |
   +===============+===========+=========================================+
   | id            |           | Any unique value for the request,       |
   |               |           | including a hash, checksum, or uuid.    |
   +---------------+-----------+-----------------------------------------+
   | name          | powerd    |                                         |
   |               |           |                                         |
   +---------------+-----------+-----------------------------------------+
   | namespace     | sysadm    |                                         |
   |               |           |                                         |
   +---------------+-----------+-----------------------------------------+
   | action        |           | list_options, list_status,              |
   |               |           | read_options, set_active, set_inactive, |
   |               |           | set_options, start, stop.               |
   +---------------+-----------+-----------------------------------------+

The rest of this section provides examples of the available *actions*
for each type of request, along with their responses.

.. index:: powerd listoptions
.. _powerd list options:

List Options
============

The :command:`list_options` action lists all the available options and
possible settings for each one.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "list_options"
   }

**WebSocket Request**

.. code-block:: json

   {
      "name" : "powerd",
      "namespace" : "sysadm",
      "args" : {
         "action" : "list_options"
      },
      "id" : "fooid"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "list_options": {
         "ac_power_mode": [
           "maximum",
           "hiadaptive",
           "adaptive",
           "minumum"
         ],
         "adaptive_lower_threshold_percent": "int min=1 max=100",
         "adaptive_raise_threshold_percent": "int min=1 max=100",
         "battery_power_mode": [
           "maximum",
           "hiadaptive",
           "adaptive",
           "minumum"
         ],
         "max_cpu_freq": "int frequency(hz)>0",
         "min_cpu_freq": "int frequency(hz)>0",
         "polling_interval_ms": "int milliseconds>0",
         "unknown_power_mode": [
           "maximum",
           "hiadaptive",
           "adaptive",
           "minumum"
         ]
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd liststatus
.. _list status:

List Status
===========

The :command:`list_status` command displays the current state of the
service (running, enabled, etc).

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "list_status"
   }

**WebSocket Request**

.. code-block:: json

   {
      "id" : "fooid",
      "name" : "powerd",
      "namespace" : "sysadm",
      "args" : {
         "action" : "list_status"
      }
   }

**Response**

.. code-block:: json

   {
     "args": {
       "list_status": {
         "enabled": "true",
         "running": "true"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd readoptions
.. _read options:

Read Options
============

The :command:`read_options` command shows all the current **powerd**
settings.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "read_options"
   }

**WebSocket Request**

.. code-block:: json

   {
      "id" : "fooid",
      "name" : "powerd",
      "args" : {
         "action" : "read_options"
      },
      "namespace" : "sysadm"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "read_options": {
         "ac_power_mode": "maximum",
         "adaptive_lower_threshold_percent": "50",
         "adaptive_raise_threshold_percent": "75",
         "battery_power_mode": "adaptive",
         "max_cpu_freq": "-1",
         "min_cpu_freq": "-1",
         "polling_interval_ms": "250",
         "unknown_power_mode": "adaptive"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd setactive
.. _set active:

Set Active
==========

The :command:`set_active` command enables the specified device to start
on bootup.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "set_active"
   }

**WebSocket Request**

.. code-block:: json

   {
      "args" : {
         "action" : "set_active"
      },
      "id" : "fooid",
      "namespace" : "sysadm",
      "name" : "powerd"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "set_active": {
         "enabled": "true"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd set inactive
.. _set inactive:

Set Inactive
============

The :command:`set_inactive` command disables the specific device from
starting on bootup.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "set_inactive"
   }

**WebSocket Request**

.. code-block:: json

   {
      "args" : {
         "action" : "set_inactive"
      },
      "id" : "fooid",
      "namespace" : "sysadm",
      "name" : "powerd"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "set_inactive": {
         "disabled": "true"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd set options
.. _set options:

Set Options
===========

Use the :command:`set_options` command to modify any **powerd**
settings.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "battery_power_mode" : "minimum",
      "action" : "set_options"
   }

**WebSocket Request**

.. code-block:: json

   {
      "name" : "powerd",
      "args" : {
         "action" : "set_options",
         "battery_power_mode" : "minimum"
      },
      "id" : "fooid",
      "namespace" : "sysadm"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "set_options": {
         "ac_power_mode": "maximum",
         "adaptive_lower_threshold_percent": "50",
         "adaptive_raise_threshold_percent": "75",
         "battery_power_mode": "minimum",
         "max_cpu_freq": "-1",
         "min_cpu_freq": "-1",
         "polling_interval_ms": "250",
         "unknown_power_mode": "adaptive"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd start
.. _powerd start:

Start
=====

The :command:`start` command starts the service immediately.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "start"
   }

**WebSocket Request**

.. code-block:: json

   {
      "args" : {
         "action" : "start"
      },
      "id" : "fooid",
      "namespace" : "sysadm",
      "name" : "powerd"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "start": {
         "started": "true"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }

.. index:: powerd stop
.. _powerd stop:

Stop
====

The :command:`stop` command immediately stops the service.

**REST Request**

.. code-block:: none

   PUT /sysadm/powerd
   {
      "action" : "stop"
   }

**WebSocket Request**

.. code-block:: json

   {
      "args" : {
         "action" : "stop"
      },
      "id" : "fooid",
      "namespace" : "sysadm",
      "name" : "powerd"
   }

**Response**

.. code-block:: json

   {
     "args": {
       "stop": {
         "stopped": "true"
       }
     },
     "id": "fooid",
     "name": "response",
     "namespace": "sysadm"
   }
