.. index:: iocage class
.. _iocage:

iocage
******

The iocage class is used to manage jails, which provide a light-weight,
operating system-level virtualization for running applications or
services.

Every iocage class request contains these parameters:

+-----------+-----------+----------------------------------------------+
| Parameter | Value     | Description                                  |
|           |           |                                              |
+===========+===========+==============================================+
| id        |           | Any unique value for the request,            |
|           |           | including a hash, checksum, or uuid.         |
+-----------+-----------+----------------------------------------------+
| name      | iocage    |                                              |
|           |           |                                              |
+-----------+-----------+----------------------------------------------+
| namespace | sysadm    |                                              |
|           |           |                                              |
+-----------+-----------+----------------------------------------------+
| action    |           | "activatepool", "activatestatus",            |
|           |           | "cleanreleases", "cleantemplates",           |
|           |           | "createplugin", "deactivatepool",            |
|           |           | "fetchreleases", "listjails", "listplugins", |
|           |           | "listreleases", "listtemplates"              |
+-----------+-----------+----------------------------------------------+

The rest of this section provides examples of the available *actions*
for each type of request, along with their responses.

.. index:: iocage activatepool
.. _Activate a Pool:

Activate a Pool
===============

The :command:`activatepool` action can be used to specify the ZFS pool
to store jails. If a pool is not specified, the response indicates
the current setting.

These examples specify the pool to use:

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "activatepool",
   "pool" : "tank1"
 }

**WebSocket Request**

.. code-block:: json

 {
   "name" : "iocage",
   "args" : {
     "pool" : "tank1",
     "action" : "activatepool"
   },
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "activatepool": {
       "success": "pool tank1 activated."
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

These examples show responses when the pool is not specified:

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
    "action" : "activatepool"
 }

**REST Response**

.. code-block:: json

 {
   "args": {
     "activatepool": {
       "currently active": {
         "pool": " tank"
       }
     }
   }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
     "action" : "activatepool"
   },
   "namespace" : "sysadm",
   "name" : "iocage",
   "id" : "fooid"
 }

**WebSocket Response**

.. code-block:: json

 {
   "args": {
     "activatepool": {
       "currently active": {
         "pool": " tank"
       }
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage activatestatus
.. _Activate Status:

Activate Status
===============

This lists the currently activated pool for iocage to use.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "activatestatus"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
     "action" : "activatestatus"
   },
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
   "args": {
    "activatestatus":{
       "activated":"true",
       "pool":"my_zpool"
     }
   }
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage cleanreleases
.. _Clean Releases:

Clean Releases
==============

:command:`cleanreleases` removes all the RELEASES downloaded or cached on the local system.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "cleanreleases"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
     "action" : "cleanreleases"
   },
   "id" : "fooid",
   "name" : "iocage"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "cleanreleases": {
      "success": "All RELEASEs have been cleaned."
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage cleantemplates
.. _Clean Templates:

Clean Templates
===============

:command:`cleantemplates` deletes all cached templates from the local system.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "cleantemplates"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
      "action" : "cleantemplates"
   },
   "id" : "fooid",
   "name" : "iocage"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "cleantemplates": {
       "success": "All templates have been cleaned."
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage createplugin
.. _Create Plugin:

Create Plugin
=============

:command:`createplugin` fetches and creates a new plugin jail. There are
some required arguments:

.. code-block:: none

 "action"="createplugin"
 "plugin"="name_of_plugin"
 "net_device"="network_device_to_use"
 "ip4" *or* "ip6" with the address to assign to the new jail (IPv4 or IPv6 address)

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "plugin" : "gitlab",
   "net_device" : "re0",
   "action" : "createplugin",
   "ip4" : "10.20.0.130"
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "name" : "iocage",
   "args" : {
      "ip4" : "10.20.0.130",
      "plugin" : "gitlab",
      "net_device" : "re0",
      "action" : "createplugin"
   },
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "createplugin": {
       "started_dispatcher_id": "sysadm_iocage_fetch_plugin_gitlab"
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage deactivatepool
.. _Deactivate a Pool:

Deactivate a Pool
=================

Since only one pool can be active, the :command:`"deactivatepool"`
action is used to deactivate a currently active pool. Run this action
before using :command:`"activatepool"` to activate a different pool.
When a pool is deactivated, no data is removed. However, you won't have
access to its jails unless you move those datasets to the newly
activated pool or activate the old pool again.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "pool" : "tank1",
   "action" : "deactivatepool"
 }

**WebSocket Request**

.. code-block:: json

 {
   "name" : "iocage",
   "args" : {
     "action" : "deactivatepool",
     "pool" : "tank1"
   },
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "deactivatepool": {
      "success": "pool tank1 deactivated."
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage fetchreleases
.. _Fetch Releases:

Fetch Releases
==============

:command:`fetchreleases` pulls any remotely available FreeBSD releases and either updates or caches
them on the local system for use when creating jails.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "fetchreleases",
   "releases" : [
     "10.3-RELEASE",
     "10.2-RELEASE"
   ]
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
     "releases" : [
       "10.3-RELEASE",
       "10.2-RELEASE"
       ],
     "action" : "fetchreleases"
   },
   "name" : "iocage",
   "namespace" : "sysadm",
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "fetchreleases": {
       "started_dispatcher_id": [
         "sysadm_iocage_fetch_release_10.3-RELEASE",
         "sysadm_iocage_fetch_release_10.2-RELEASE"
       ]
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage listjails
.. _List Jails:

List Jails
==========

:command:`listjails` displays all current jails on the system.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "listjails"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
     "action" : "listjails"
   },
   "name" : "iocage",
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "listjails":{
       "jails":{
         "jid_1":{
           "jid" : "jail_id",
           "uuid": "unique_id_string",
           "boot": "on/off",
           "state":"jail_state",
           "tag":"jail_tag",
           "type":"jail_type",
           "release":"freebsd_release",
           "ip4":"ipv4_address",
           "ip6":"ipv6_address",
           "template":"template_1"
         },
         "jid_2":{
           "jid" : "jail_id",
           "uuid": "unique_id_string",
           "boot": "on/off",
           "state":"jail_state",
           "tag":"jail_tag",
           "type":"jail_type",
           "release":"freebsd_release",
           "ip4":"ipv4_address",
           "ip6":"ipv6_address",
           "template":"template_1"
           }
       }
     }
   }
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage listplugins
.. _List Plugins:

List Plugins
============

The "listplugins" action shows all available plugins for *iocage*.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "listplugins"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
     "action" : "listplugins"
   },
   "name" : "iocage",
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "listplugins":{
       "remote" : {
         "btsync": {
           "description": "Resilient, fast and scalable file sync software for enterprises and individuals.",
           "id": "btsync",
           "name": "BitTorrent Sync"
         },
         "couchpotato": {
           "description": "CouchPotato is an automatic NZB and torrent downloader.",
           "id": "couchpotato",
           "name": "CouchPotato"
         },
         "crashplan": {
           "description": "Computer backup and data storage made simple.",
           "id": "crashplan",
           "name": "Crashplan"
         },
         "deluge": {
           "description": "Bittorrent client using Python, and libtorrent-rasterbar",
           "id": "deluge",
           "name": "Deluge"
         },
         "emby": {
           "description": "Home media server built using mono and other open source technologies",
           "id": "emby",
           "name": "Emby"
         },
         "gitlab": {
           "description": "Powerful features for modern software development",
           "id": "gitlab",
           "name": "GitLab"
         },
         "jenkins": {
           "description": "Jenkins CI",
           "id": "jenkins",
           "name": "Jenkins"
         }
        },
       "local" : {
         "pluginname_jid" : {
           "jid" : "number",
           "uuid" : "uuid_string",
           "boot" : "on/off",
           "state" : "activestate",
           "tag" : "pluginname",
           "type" : "plugin",
           "release" : "freebsd_release",
           "ip4" : "ipv4_address",
           "ip6" : "ipv6_address",
           "template" : "-"
         }
       }
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage listreleases
.. _List Releases:

List Releases
=============

The "listreleases action displays all supported FreeBSD releases for
iocage jails.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "listreleases"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
     "action" : "listreleases"
   },
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "listreleases": {
       "local": [
         ""
       ],
       "remote": [
         "9.3-RELEASE (EOL)",
         "10.1-RELEASE (EOL)",
         "10.2-RELEASE (EOL)",
         "10.3-RELEASE",
         "11.0-RELEASE"
       ]
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: iocage listtemplates
.. _List Templates:

List Templates
==============

:command:`listtemplates` displays all jail templates available on the local system.

**REST Request**

.. code-block:: none

 PUT /sysadm/iocage
 {
   "action" : "listtemplates"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
     "action" : "listtemplates"
   },
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
   "args": {
     "listtemplates":{
       "templates" : {
         "template_1" : {
         "jid" : "jail_id",
         "uuid": "unique_id_string",
         "boot": "on/off",
         "state":"jail_state",
         "tag":"jail_tag",
         "type":"jail_type",
         "release":"freebsd_release",
         "ip4":"ipv4_address",
         "ip6":"ipv6_address",
         "template":"template_1"
         }
       }
     }
   }
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }
