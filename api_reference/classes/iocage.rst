.. warning:: Most iocage class actions are deactivated due to a rework
   of iocage. The actions are being re-enabled as the iocage changes are
   added to |sysadm|. As of 5/31/17, **"activatepool"**,
   **"deactivatepool"**, **"listplugins"**, and **"listreleases"** are
   the only functional actions.

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
| action    |           | Actions include "activatepool", "capjail",   |
|           |           | "cleanall", "cleanjails", "cleanreleases",   |
|           |           | "cleantemplates", "clonejail", "createjail", |
|           |           | "deactivatepool", "destroyjail", "df",       |
|           |           | "execjail", "getjailsettings", "listjails",  |
|           |           | "listplugins", "listreleases", "startjail",  |
|           |           | and "stopjail".                              |
+-----------+-----------+----------------------------------------------+

The rest of this section provides examples of the available *actions*
for each type of request, along with their responses.

.. index:: iocage listreleases
.. _List Releases:

List Releases
=============

The "listreleases action displays all supported FreeBSD releases for
iocage jails.

**REST Request**

::

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

.. index:: iocage listplugins
.. _List Plugins:

List Plugins
============

The "listplugins" action shows all available plugins for *iocage*.

**REST Request**

::

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
     "listplugins": {
       "remote": {
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
         },
         "jenkins-lts": {
           "description": "Jenkins CI (Long Term Support Version)",
           "id": "jenkins-lts",
           "name": "Jenkins (LTS)"
         },
         "madsonic": {
           "description": "Open-source web-based media streamer and jukebox.",
           "id": "madsonic",
           "name": "MadSonic"
         },
         "nextcloud": {
           "description": "Access, share and protect your files, calendars, contacts, communication & more at home and in your enterprise.",
           "id": "nextcloud",
           "name": "NextCloud"
         },
         "plexmediaserver": {
           "description": "The Plex media server system",
           "id": "plexmediaserver",
           "name": "Plex Media Server"
         },
         "plexmediaserver-plexpass": {
           "description": "The Plex media server system",
           "id": "plexmediaserver-plexpass",
           "name": "Plex Media Server (PlexPass)"
         },
         "quasselcore": {
           "description": "Quassel Core is a daemon/headless IRC client, part of Quassel, that supports 24/7 connectivity. Quassel Client can be attached to it to.",
           "id": "quasselcore",
           "name": "Quasselcore"
         },
         "sickrage": {
           "description": "Automatic Video Library Manager for TV Shows",
           "id": "sickrage",
           "name": "SickRage"
         },
         "sonarr": {
           "description": "PVR for Usenet and BitTorrent users",
           "id": "sonarr",
           "name": "Sonarr"
         },
         "subsonic": {
           "description": "Open-source web-based media streamer and jukebox.",
           "id": "subsonic",
           "name": "SubSonic"
         },
         "syncthing": {
           "description": "Personal cloud sync",
           "id": "syncthing",
           "name": "Syncthing"
         },
         "transmission": {
           "description": "Fast and lightweight daemon BitTorrent client",
           "id": "transmission",
           "name": "Transmission"
         }
       }
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

The "listjails" action lists information about currently installed
jails. For each jail, the response includes the UUID of the jail,
whether or not the jail has been configured to start at system boot,
the jail ID (only applies to running jails), whether or not the jail is
running, a friendly name for the jail (tag), and the type of jail
(basejail or thickjail).

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "listjails"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "listjails": {
            "611c89ae-c43c-11e5-9602-54ee75595566": {
                "boot": "off",
                "ip4": "-",
                "jid": "-",
                "state": "down",
                "tag": "testjail",
                "type": "basejail"
            }
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "action" : "listjails"
   },
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "listjails": {
      "611c89ae-c43c-11e5-9602-54ee75595566": {
        "boot": "off",
        "ip4": "-",
        "jid": "-",
        "state": "down",
        "tag": "testjail",
        "type": "basejail"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage getjailsettings
.. _Jail Settings:

Jail Settings
=============

The "getjailsettings" action lists settings that apply to the specified
jail. This action supports 4 modes:

* Specify a property and a jail.

* Specify a property and *-r* for all downloaded releases.

* Specify *all* properties for the specified jail.

* Specify the jail.

Here is an example of specifying the property and the jail:

**REST Request**

::

 PUT /sysadm/iocage
 {
   "jail" : "test",
   "action" : "getjailsettings",
   "prop" : "vnet"
 }

**WebSocket Request**

.. code-block:: json

 {
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm",
   "args" : {
      "prop" : "vnet",
      "action" : "getjailsettings",
      "jail" : "test"
   }
 }

**Response**

.. code-block:: json

 {
  "args": {
    "getjailsettings": {
      "test": {
        "vnet": "off"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

Here is an example of using *-r* and a specifed property:

**REST Request**

::

 PUT /sysadm/iocage
 {
   "switches" : "-r",
   "prop" : "vnet",
   "action" : "getjailsettings"
 }

**WebSocket Request**

.. code-block:: json

 {
   "name" : "iocage",
   "namespace" : "sysadm",
   "args" : {
      "prop" : "vnet",
      "action" : "getjailsettings",
      "switches" : "-r"
   },
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "getjailsettings": {
      "9b8e1033-d065-11e5-8209-d05099728dbf": {
        "TAG": "test",
        "vnet": "off"
      },
      "b67065a9-cfb9-11e5-8209-d05099728dbf": {
        "TAG": "2016-02-09@23:47:04",
        "vnet": "off"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

An example of specifying either *all* and a jail, or just specifying the
jail, as both modes produce identical outputs:

**REST Request**

::

 PUT /sysadm/iocage
 {
   "jail" : "test",
   "action" : "getjailsettings",
   "prop" : "all"
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "name" : "iocage",
   "namespace" : "sysadm",
   "args" : {
      "jail" : "test",
      "action" : "getjailsettings",
      "prop" : "all"
   }
 }

**Response**

.. code-block:: json

 {
  "args": {
    "getjailsettings": {
      "test": {
        "allow_chflags": "0",
        "allow_mount": "0",
        "allow_mount_devfs": "0",
        "allow_mount_nullfs": "0",
        "allow_mount_procfs": "0",
        "allow_mount_tmpfs": "0",
        "allow_mount_zfs": "0",
        "allow_quotas": "0",
        "allow_raw_sockets": "0",
        "allow_set_hostname": "1",
        "allow_socket_af": "0",
        "allow_sysvipc": "0",
        "available": "83.4G",
        "boot": "off",
        "bpf": "off",
        "branch": "-",
        "children_max": "0",
        "compression": "lz4",
        "compressratio": "2.27x",
        "coredumpsize": "off",
        "count": "1",
        "cpuset": "off",
        "cputime": "off",
        "datasize": "off",
        "dedup": "off",
        "defaultrouter": "none",
        "defaultrouter6": "none",
        "devfs_ruleset": "4",
        "dhcp": "off",
        "enforce_statfs": "2",
        "exec_clean": "1",
        "exec_fib": "0",
        "exec_jail_user": "root",
        "exec_poststart": "/usr/bin/true",
        "exec_poststop": "/usr/bin/true",
        "exec_prestart": "/usr/bin/true",
        "exec_prestop": "/usr/bin/true",
        "exec_start": "/bin/sh /etc/rc",
        "exec_stop": "/bin/sh /etc/rc.shutdown",
        "exec_system_jail_user": "0",
        "exec_system_user": "root",
        "exec_timeout": "60",
        "ftpdir": "-",
        "ftpfiles": "-",
        "ftphost": "-",
        "ftplocaldir": "-",
        "gitlocation": "https",
        "hack88": "0",
        "host_domainname": "none",
        "host_hostname": "9b8e1033-d065-11e5-8209-d05099728dbf",
        "host_hostuuid": "9b8e1033-d065-11e5-8209-d05099728dbf",
        "hostid": "a60db2df-3c0e-11e5-8986-d05099728dbf",
        "interfaces": "vnet0",
        "ip4": "new",
        "ip4_addr": "none",
        "ip4_autoend": "none",
        "ip4_autostart": "none",
        "ip4_autosubnet": "none",
        "ip4_saddrsel": "1",
        "ip6": "new",
        "ip6_addr": "none",
        "ip6_saddrsel": "1",
        "istemplate": "no",
        "jail_zfs": "off",
        "jail_zfs_dataset": "iocage/jails/9b7f1420-d065-11e5-8209-d05099728dbf/data",
        "jail_zfs_mountpoint": "none",
        "last_started": "2016-02-10_20",
        "login_flags": "-f root",
        "maxproc": "off",
        "memorylocked": "off",
        "memoryuse": "8G",
        "mount_devfs": "1",
        "mount_fdescfs": "1",
        "mount_linprocfs": "0",
        "mount_procfs": "0",
        "mountpoint": "/iocage/jails/9b8e1033-d065-11e5-8209-d05099728dbf",
        "msgqqueued": "off",
        "msgqsize": "off",
        "nmsgq": "off",
        "notes": "none",
        "nsemop": "off",
        "nshm": "off",
        "nthr": "off",
        "openfiles": "off",
        "origin": "-",
        "owner": "root",
        "pcpu": "off",
        "pkglist": "none",
        "priority": "99",
        "pseudoterminals": "off",
        "quota": "none",
        "release": "10.2-RELEASE",
        "reservation": "none",
        "resolver": "none",
        "rlimits": "off",
        "securelevel": "2",
        "shmsize": "off",
        "stacksize": "off",
        "start": "-",
        "stop_timeout": "30",
        "swapuse": "off",
        "sync_stat": "-",
        "sync_target": "none",
        "sync_tgt_zpool": "none",
        "tag": "test",
        "template": "-",
        "type": "basejail",
        "used": "1.76M",
        "vmemoryuse": "off",
        "vnet": "off",
        "vnet0_mac": "none",
        "vnet1_mac": "none",
        "vnet2_mac": "none",
        "vnet3_mac": "none",
        "wallclock": "off"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage df
.. _List Resource Usage:

List Resource Usage
===================

The "df" action lists resource usage for all jails. For each jail, the
response includes: CRT (compression ratio), RES (reserved space), QTA
(disk quota), USE (used space), AVA (available space), and TAG (jail
name).

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "df"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "name" : "iocage",
   "id" : "fooid",
   "args" : {
      "action" : "df"
   }
 }

**Response**

.. code-block:: json

 {
  "args": {
    "df": {
      "f250ab25-d062-11e5-8209-d05099728dbf": {
        "ava": "83.4G",
        "crt": "2.30x",
        "qta": "none",
        "res": "none",
        "tag": "test",
        "use": "1.69M"
      },
      "f39318ae-d064-11e5-8209-d05099728dbf": {
        "ava": "83.4G",
        "crt": "2.30x",
        "qta": "none",
        "res": "none",
        "tag": "test2",
        "use": "1.69M"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage startjail
.. _Start a Jail:

Start a Jail
============

The "startjail" action starts the specified jail.

.. warning:: A jail can be started only once. If the jail is already
   running, an error message will be generated.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "startjail",
   "jail" : "test"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "startjail": {
            "test": {
                "* Starting 0bf985de-ca0f-11e5-8d45-d05099728dbf (test)": "",
                "+ Started (shared IP mode) OK": "",
                "+ Starting services OK": ""
            }
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "id" : "fooid",
   "args" : {
      "action" : "startjail",
      "jail" : "test"
   },
   "name" : "iocage"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "startjail": {
      "test": {
        "INFO": " 0bf985de-ca0f-11e5-8d45-d05099728dbf (test) is already up"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage stopjail
.. _Stop a Jail:

Stop a Jail
===========

The "stopjail" action stops the specified jail.

.. warning:: A jail can be only stopped once. If the jail has already
   stopped, an error message will be generated.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "stopjail",
   "jail" : "test"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "stopjail": {
            "test": {
                "* Stopping 0bf985de-ca0f-11e5-8d45-d05099728dbf (test)": "",
                "+ Removing jail process OK": "",
                "+ Running post-stop OK": "",
                "+ Running pre-stop OK": "",
                "+ Stopping services OK": ""
            }
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "jail" : "test",
      "action" : "stopjail"
   },
   "namespace" : "sysadm",
   "id" : "fooid",
   "name" : "iocage"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "stopjail": {
      "test": {
        "INFO": " 0bf985de-ca0f-11e5-8d45-d05099728dbf (test) is already down"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage capjail
.. _Cap a Jail:

Cap a Jail
===========

The "capjail" action re-applies resource limits to a running jail. Use
this action when you make a change to the specified jail's resources and
want to apply the changes without restarting the jail.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "jail" : "test",
   "action" : "capjail"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "jail" : "test",
      "action" : "capjail"
   },
   "namespace" : "sysadm",
   "name" : "iocage",
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "capjail": {
      "success": "jail test capped."
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage clonejail
.. _Clone a Jail:

Clone a Jail
============

The "clonejail" action clones the specified "jail". By default, the
clone will inherit that jail's properties. Use "props" to specify any
properties that should differ. All available properties are described in
`iocage(8) <https://github.com/iocage/iocage/blob/master/iocage.8.txt>`_.

In this example, the "tag" property is specified so that the new jail
has a different name than the jail it was cloned from.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "props" : "tag=newtest",
   "jail" : "test",
   "action" : "clonejail"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "name" : "iocage",
   "args" : {
      "action" : "clonejail",
      "jail" : "test",
      "props" : "tag=newtest"
   },
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "clonejail": {
      "jail": "test",
      "props": "tag=newtest",
      "success": {
        "Successfully created": " 5e1fe97e-cfba-11e5-8209-d05099728dbf (newtest)"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

In this example, no properties are specified so iocage populates its own
values and the props returned in the response is empty:

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "clonejail",
   "jail" : "test"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "jail" : "test",
      "action" : "clonejail"
   },
   "name" : "iocage",
   "namespace" : "sysadm",
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "clonejail": {
      "jail": "test",
      "props": "",
      "success": {
        "Successfully created": " 89e78032-cfba-11e5-8209-d05099728dbf (2016-02-09@23"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage createjail
.. _Create a Jail:

Create a Jail
=============

The "createjail" action creates a jail.

In this example, the "tag" property sets the name of the new jail and
the "release" property specifies which template to use.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "createjail",
   "props" : "tag=test release=10.2-RELEASE"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "props" : "tag=test release=10.2-RELEASE",
      "action" : "createjail"
   },
   "namespace" : "sysadm",
   "name" : "iocage",
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "createjail": {
      "props": "tag=test release=10.2-RELEASE",
      "success": {
        "Successfully created": " 3030c554-d05e-11e5-8209-d05099728dbf (test)"
      },
      "switches": ""
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

In this example, the **-e** switch, which creates an empty jail, is
specified using "switches". Refer to
`iocage(8) <https://github.com/iocage/iocage/blob/master/iocage.8.txt>`_
for the list of available switches.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "switches" : "-e",
   "action" : "createjail",
   "props" : "tag=emptytest"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
      "props" : "tag=emptytest",
      "action" : "createjail",
      "switches" : "-e"
   },
   "name" : "iocage",
   "id" : "fooid"
 }

**Response**

::

 {
  "args": {
    "createjail": {
      "props": "tag=emptytest",
      "success": {
        "uuid": "1325b8bc-d05e-11e5-8209-d05099728dbf"
      },
      "switches": "-e"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage destroyjail
.. _Destroy a Jail:

Destroy a Jail
==============

The "destroyjail" action destroys the specified jail. This action is
irreversible and does not prompt for confirmation, but will fail if the
jail is running.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "destroyjail",
   "jail" : "test"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "action" : "destroyjail",
      "jail" : "test"
   },
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "destroyjail": {
      "success": {
        "Destroying": " 3030c554-d05e-11e5-8209-d05099728dbf"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage execjail
.. _Run Command:

Run Command
===========

The "execjail" action executes the specified "command" under the
privileges of the specified "user" in the specified "jail". The response
will indicate whether or not command execution succeeded as well as any
output from the command.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "execjail",
   "jail" : "test",
   "command" : "echo hi",
   "user" : "root"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "name" : "iocage",
   "args" : {
      "user" : "root",
      "action" : "execjail",
      "jail" : "test",
      "command" : "echo hi"
   },
   "id" : "fooid"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "execjail": {
      "success": {
        "hi": ""
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage cleanjails
.. _Clean Jails:

Clean Jails
===========

The "cleanjails" action destroys all existing jail datasets, including
all data stored in the jails.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "cleanjails"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
      "action" : "cleanjails"
   },
   "id" : "fooid",
   "name" : "iocage"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "cleanjails": {
      "success": "All jails have been cleaned."
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: iocage cleanreleases
.. _Clean Releases:

Clean Releases
==============

The "cleanreleases" action deletes all releases that have been fetched.
Since basejails rely on releases, do not run this action if any
basejails still exist.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "cleanreleases"
 }

**WebSocket Request**

**REST Request**

.. code-block:: json

 {
   "id" : "fooid",
   "namespace" : "sysadm",
   "args" : {
      "action" : "cleanreleases"
   },
   "name" : "iocage"
 }

**Response**

**REST Request**

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

The "cleantemplates" action destroys all existing jail templates.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "cleantemplates"
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "action" : "cleantemplates"
   },
   "name" : "iocage",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**Response**

::

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

.. index:: iocage cleanall
.. _Clean All:

Clean All
=========

The "cleanall" action destroys everything associated with iocage.

**REST Request**

::

 PUT /sysadm/iocage
 {
   "action" : "cleanall"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
      "action" : "cleanall"
   },
   "id" : "fooid",
   "name" : "iocage"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "cleanall": {
      "success": "All iocage datasets have been cleaned."
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

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

::

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
