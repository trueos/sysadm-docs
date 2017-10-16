.. index:: systemmanager class
.. _systemmanager:

systemmanager
*************

The systemmanager class is used to retrieve information about the
system. Every systemmanager class request contains several parameters:

.. tabularcolumns:: |>{\RaggedRight}p{\dimexpr 0.15\linewidth-2\tabcolsep}
                    |>{\RaggedRight}p{\dimexpr 0.15\linewidth-2\tabcolsep}
                    |>{\RaggedRight}p{\dimexpr 0.70\linewidth-2\tabcolsep}|

.. table:: systemmanager class overview
   :class: longtable

   +-----------+---------------+---------------------------------------+
   | Parameter | Value         | Description                           |
   |           |               |                                       |
   +===========+===============+=======================================+
   | id        |               | Any unique value for the request,     |
   |           |               | including a hash, checksum, or uuid.  |
   +-----------+---------------+---------------------------------------+
   | name      | systemmanager |                                       |
   |           |               |                                       |
   +-----------+---------------+---------------------------------------+
   | namespace | sysadm        |                                       |
   |           |               |                                       |
   +-----------+---------------+---------------------------------------+
   | action    |               | Actions include "batteryinfo",        |
   |           |               | "cpupercentage", "cputemps",          |
   |           |               | "deviceinfo", "externalmounts",       |
   |           |               | "fetch_ports", "halt",                |
   |           |               |  "killproc", "memorystats",           |
   |           |               | "procinfo", "reboot", "setsysctl",    |
   |           |               | "sysctllist", and "systemmanager".    |
   +-----------+---------------+---------------------------------------+

The rest of this section provides examples of the available *actions*
for each type of request, along with their responses.

.. index:: systemmanager batteryinfo
.. _Battery Information:

Battery Information
===================

The :command:`"batteryinfo"` action indicates whether or not a battery
exists. If it does, it also reports the battery's current charge
percentage level (1-99), its status (*offline*, *charging*, *on backup*,
or *unknown*), and estimated time left in seconds.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "batteryinfo"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "batteryinfo": {
            "battery": "false"
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "name" : "systemmanager",
   "id" : "fooid",
   "args" : {
      "action" : "batteryinfo"
   }
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "batteryinfo": {
      "battery": "false"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager cpupercentage
.. _CPU Usage:

CPU Usage
=========

The :command:`"cpupercentage"` action returns the usage percentage of
each CPU.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "cpupercentage"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "cpupercentage": {
            "busytotal": "28",
            "cpu1": {
                "busy": "28"
            },
            "cpu2": {
                "busy": "31"
            },
            "cpu3": {
                "busy": "29"
            },
            "cpu4": {
                "busy": "24"
            }
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "action" : "cpupercentage"
   },
   "name" : "systemmanager",
   "id" : "fooid",
   "namespace" : "sysadm"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "cpupercentage": {
      "busytotal": "28",
      "cpu1": {
        "busy": "28"
      },
      "cpu2": {
        "busy": "31"
      },
      "cpu3": {
        "busy": "29"
      },
      "cpu4": {
        "busy": "24"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager cputemps
.. _CPU Temperature:

CPU Temperature
===============

The :command:`"cputemps"` action returns the temperature of each CPU.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "cputemps"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "cputemps": {
            "cpu0": "27.0C",
            "cpu1": "34.0C",
            "cpu2": "33.0C",
            "cpu3": "31.0C"
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "action" : "cputemps"
   },
   "id" : "fooid",
   "name" : "systemmanager",
   "namespace" : "sysadm"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "cputemps": {
      "cpu0": "34.0C",
      "cpu1": "32.0C",
      "cpu2": "34.0C",
      "cpu3": "31.0C"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager deviceinfo
.. _Device Information:

Device Information
==================

:command:`"deviceinfo"` returns the full information about all devices
attached to the system using :command:`pciconf -lv`.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
    "action" : "deviceinfo"
 }

**WebSocket Request**

.. code-block:: json

 {
    "id" : "fooid",
    "name" : "systemmanager",
    "namespace" : "sysadm",
    "args" : {
       "action" : "deviceinfo"
    }
 }

**Response**

.. code-block:: json

 {
   "args": {
     "deviceinfo": {
       "ahci0": {
         "class": "mass storage",
         "device": "8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode]",
         "subclass": "SATA",
         "vendor": "Intel Corporation"
       },
       "ehci0": {
         "class": "serial bus",
         "device": "8 Series/C220 Series Chipset Family USB EHCI",
         "subclass": "USB",
         "vendor": "Intel Corporation"
       },
       "ehci1": {
         "class": "serial bus",
         "device": "8 Series/C220 Series Chipset Family USB EHCI",
         "subclass": "USB",
         "vendor": "Intel Corporation"
       },
       "hdac0": {
         "class": "multimedia",
         "subclass": "HDA",
         "vendor": "NVIDIA Corporation"
       },
       "hdac1": {
         "class": "multimedia",
         "device": "8 Series/C220 Series Chipset High Definition Audio Controller",
         "subclass": "HDA",
         "vendor": "Intel Corporation"
       },
       "hostb0": {
         "class": "bridge",
         "device": "4th Gen Core Processor DRAM Controller",
         "subclass": "HOST-PCI",
         "vendor": "Intel Corporation"
       },
       "isab0": {
         "class": "bridge",
         "device": "B85 Express LPC Controller",
         "subclass": "PCI-ISA",
         "vendor": "Intel Corporation"
       },
       "none0": {
         "class": "simple comms",
         "device": "8 Series/C220 Series Chipset Family MEI Controller",
         "vendor": "Intel Corporation"
       },
       "none1": {
         "class": "serial bus",
         "device": "8 Series/C220 Series Chipset Family SMBus Controller",
         "subclass": "SMBus",
         "vendor": "Intel Corporation"
       },
       "pcib1": {
         "class": "bridge",
         "device": "Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller",
         "subclass": "PCI-PCI",
         "vendor": "Intel Corporation"
       },
       "pcib2": {
         "class": "bridge",
         "device": "8 Series/C220 Series Chipset Family PCI Express Root Port",
         "subclass": "PCI-PCI",
         "vendor": "Intel Corporation"
       },
       "pcib3": {
         "class": "bridge",
         "device": "8 Series/C220 Series Chipset Family PCI Express Root Port",
         "subclass": "PCI-PCI",
         "vendor": "Intel Corporation"
       },
       "pcib4": {
         "class": "bridge",
         "device": "8 Series/C220 Series Chipset Family PCI Express Root Port",
         "subclass": "PCI-PCI",
         "vendor": "Intel Corporation"
       },
       "pcib5": {
         "class": "bridge",
         "device": "82801 PCI Bridge",
         "subclass": "PCI-PCI",
         "vendor": "Intel Corporation"
       },
       "re0": {
         "class": "network",
         "device": "RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller",
         "subclass": "ethernet",
         "vendor": "Realtek Semiconductor Co., Ltd."
       },
       "vgapci0": {
         "class": "display",
         "device": "GM206 [GeForce GTX 960]",
         "subclass": "VGA",
         "vendor": "NVIDIA Corporation"
       },
       "xhci0": {
         "class": "serial bus",
         "device": "8 Series/C220 Series Chipset Family USB xHCI",
         "subclass": "USB",
         "vendor": "Intel Corporation"
       }
     }
   },
   "id": "fooid",
   "name": "response",
   "namespace": "sysadm"
 }

.. index:: systemmanager externalmounts
.. _List External Mounts:

List External Mounts
====================

The :command:`"externalmounts"` action returns a list of mounted
external devices. Supported device types are *UNKNOWN*, *USB*, *HDRIVE*
(external hard drive), *DVD*, and *SDCARD*. For each mounted device, the
response includes the *device name*, *filesystem*, *mount path*, and
*device type*.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "externalmounts"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "externalmounts": {
            "/dev/fuse": {
                "filesystem": "fusefs",
                "path": "/usr/home/kris/.gvfs",
                "type": "UNKNOWN"
            }
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "namespace" : "sysadm",
   "name" : "systemmanager",
   "args" : {
      "action" : "externalmounts"
   }
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "externalmounts": {
      "/dev/fuse": {
        "filesystem": "fusefs",
        "path": "/usr/home/kris/.gvfs",
        "type": "UNKNOWN"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager halt
.. _Halt the System:

.. index:: fetch_ports action
.. _Fetch Ports:

Fetch Ports
===========

The :command:`"fetch_ports"` command fetches and installs the
ports from the port tree onto the system.

The optional :command:`"ports_dir"` argument specifies the directory
to place the ports tree.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "fetch_ports"
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
      "action" : "fetch_ports"
   },
   "name" : "systemmanager",
   "id" : "fooid"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "fetch_ports": {
      "process_id": "system_fetch_ports_tree",
      "result": "process_started"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
}

Halt the System
===============

The :command:`"halt"` action shuts down the system.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "halt"
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "args" : {
      "action" : "halt"
   },
   "name" : "systemmanager",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "halt": {
      "response": "true"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager killproc
.. _Kill a Process:

Kill a Process
==============

The :command:`"killproc"` action can be used to send a specified signal
to the specified *Process ID (PID)*. These signals are supported: *INT*,
*QUIT*, *ABRT*, *KILL*, *ALRM*, or *TERM*.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "signal" : "KILL",
   "pid" : "13939",
   "action" : "killproc"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "killproc": {
            "action": "killproc",
            "pid": "13939",
            "signal": "KILL"
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "namespace" : "sysadm",
   "args" : {
      "pid" : "13939",
      "action" : "killproc",
      "signal" : "KILL"
   },
   "id" : "fooid",
   "name" : "systemmanager"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "killproc": {
      "action": "killproc",
      "pid": "13939",
      "signal": "KILL"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager memorystats
.. _Memory Statistics:

Memory Statistics
=================

The :command:`"memorystats"` action returns memory statistics, including
the amount of *active*, *cached*, *free*, *inactive*, and
*total physical (wired) memory*.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "memorystats"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "memorystats": {
            "active": "818",
            "cache": "69",
            "free": "4855",
            "inactive": "2504",
            "wired": "1598"
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "args" : {
      "action" : "memorystats"
   },
   "namespace" : "sysadm",
   "name" : "systemmanager"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "memorystats": {
      "active": "826",
      "cache": "69",
      "free": "4847",
      "inactive": "2505",
      "wired": "1598"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager procinfo
.. _Process Information:

Process Information
===================

The :command:`"procinfo"` action lists information about each running
process. Because a system has many running processes, the responses in
this section only show one process as an example of the type of
information listed by this action.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "procinfo"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "procinfo": {
                  "228": {
        "command": "adjkerntz",
        "cpu": "3",
        "nice": "0",
        "pri": "52",
        "res": "1968K",
        "size": "8276K",
        "state": "pause",
        "thr": "1",
        "time": "0:00",
        "username": "root",
        "wcpu": "0.00%"
          }
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "namespace" : "sysadm",
   "name" : "systemmanager",
   "args" : {
      "action" : "procinfo"
   }
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "procinfo": {
      "228": {
        "command": "adjkerntz",
        "cpu": "3",
        "nice": "0",
        "pri": "52",
        "res": "1968K",
        "size": "8276K",
        "state": "pause",
        "thr": "1",
        "time": "0:00",
        "username": "root",
        "wcpu": "0.00%"
      }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager reboot
.. _Reboot the System:

Reboot the System
=================

The :command:`"reboot"` action reboots the system.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "reboot"
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "args" : {
      "action" : "reboot"
   },
   "name" : "systemmanager",
   "namespace" : "sysadm"
 }

**Response**

.. code-block:: json

 {
  "args": {
    "reboot": {
      "response": "true"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager setsysctl
.. _Set a Sysctl:

Set a Sysctl
============

The :command:`"setsysctl"` action sets the desired (and configurable)
sysctl to the specified value. The response indicates the old value is
changed to the new value.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "value" : "0",
   "sysctl" : "security.jail.mount_devfs_allowed",
   "action" : "setsysctl"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "setsysctl": {
            "response": "security.jail.mount_devfs_allowed: 1 -> 0",
            "sysctl": "security.jail.mount_devfs_allowed",
            "value": "0"
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "value" : "0",
      "action" : "setsysctl",
      "sysctl" : "security.jail.mount_devfs_allowed"
   },
   "name" : "systemmanager",
   "namespace" : "sysadm",
   "id" : "fooid"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "setsysctl": {
      "response": "security.jail.mount_devfs_allowed: 1 -> 0",
      "sysctl": "security.jail.mount_devfs_allowed",
      "value": "0"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager sysctllist
.. _List Sysctls:

List Sysctls
============

The :command:`"sysctllist"` action returns the list of all configurable
sysctl values. Since there are many, the example responses in this
section are truncated.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "sysctllist"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "sysctllist": {
            "compat.ia32.maxdsiz": "536870912",
            "compat.ia32.maxssiz": "67108864",
            "compat.ia32.maxvmem": "0",
            "compat.linux.osname": "Linux",
            "compat.linux.osrelease": "2.6.18",
            "compat.linux.oss_version": "198144",
            "compat.linux32.maxdsiz": "536870912",
            "compat.linux32.maxssiz": "67108864",
            "compat.linux32.maxvmem": "0",
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "name" : "systemmanager",
   "namespace" : "sysadm",
   "id" : "fooid",
   "args" : {
      "action" : "sysctllist"
   }
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "sysctllist": {
      "compat.ia32.maxdsiz": "536870912",
      "compat.ia32.maxssiz": "67108864",
      "compat.ia32.maxvmem": "0",
      "compat.linux.osname": "Linux",
      "compat.linux.osrelease": "2.6.18",
      "compat.linux.oss_version": "198144",
      "compat.linux32.maxdsiz": "536870912",
      "compat.linux32.maxssiz": "67108864",
      "compat.linux32.maxvmem": "0",
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: systemmanager action
.. _System Information:

System Information
==================

The :command:`"systemmanager"` action lists system information,
including the architecture, number of CPUs, type of CPU, hostname,
kernel name and version, system version and patch level, total amount of
RAM, and the system's uptime.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "systemmanager"
 }

**REST Response**

.. code-block:: json

 {
    "args": {
        "systemmanager": {
            "arch": "amd64",
            "cpucores": "4",
            "cputype": "Intel(R) Xeon(R) CPU E3-1220 v3 @ 3.10GHz",
            "hostname": "krisdesktop",
            "kernelident": "GENERIC",
            "kernelversion": "10.2-RELEASE-p11",
            "systemversion": "10.2-RELEASE-p12",
            "totalmem": 10720,
            "uptime": "up 2 days 5:09"
        }
    }
 }

**WebSocket Request**

.. code-block:: json

 {
   "args" : {
      "action" : "systemmanager"
   },
   "id" : "fooid",
   "name" : "systemmanager",
   "namespace" : "sysadm"
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "systemmanager": {
      "arch": "amd64",
      "cpucores": "4",
      "cputype": "Intel(R) Xeon(R) CPU E3-1220 v3 @ 3.10GHz",
      "hostname": "krisdesktop",
      "kernelident": "GENERIC",
      "kernelversion": "10.2-RELEASE-p11",
      "systemversion": "10.2-RELEASE-p12",
      "totalmem": 10720,
      "uptime": "up 2 days 5:09"
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }

.. index:: deviceinfo action
.. _ Device Info:

Device Info
===========

Command :command:`"deviceinfo"` returns the full information
about all devices attached to the system using :command:`pciconf -lv`.

**REST Request**

.. code-block:: none

 PUT /sysadm/systemmanager
 {
   "action" : "deviceinfo"
 }

**WebSocket Request**

.. code-block:: json

 {
   "id" : "fooid",
   "name" : "systemmanager",
   "namespace" : "sysadm",
   "args" : {
      "action" : "deviceinfo"
   }
 }

**WebSocket Response**

.. code-block:: json

 {
  "args": {
    "deviceinfo": {
      "ahci0": {
        "class": "mass storage",
        "device": "8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode]",
        "subclass": "SATA",
        "vendor": "Intel Corporation"
      },
      "ehci0": {
        "class": "serial bus",
        "device": "8 Series/C220 Series Chipset Family USB EHCI",
        "subclass": "USB",
        "vendor": "Intel Corporation"
      },
      "ehci1": {
        "class": "serial bus",
        "device": "8 Series/C220 Series Chipset Family USB EHCI",
        "subclass": "USB",
        "vendor": "Intel Corporation"
      },
      "hdac0": {
        "class": "multimedia",
        "subclass": "HDA",
        "vendor": "NVIDIA Corporation"
      },
      "hdac1": {
        "class": "multimedia",
        "device": "8 Series/C220 Series Chipset High Definition Audio Controller",
        "subclass": "HDA",
        "vendor": "Intel Corporation"
      },
      "hostb0": {
        "class": "bridge",
        "device": "4th Gen Core Processor DRAM Controller",
        "subclass": "HOST-PCI",
        "vendor": "Intel Corporation"
      },
      "isab0": {
        "class": "bridge",
        "device": "B85 Express LPC Controller",
        "subclass": "PCI-ISA",
        "vendor": "Intel Corporation"
      },
      "none0": {
        "class": "simple comms",
        "device": "8 Series/C220 Series Chipset Family MEI Controller",
        "vendor": "Intel Corporation"
      },
      "none1": {
        "class": "serial bus",
        "device": "8 Series/C220 Series Chipset Family SMBus Controller",
        "subclass": "SMBus",
        "vendor": "Intel Corporation"
      },
      "pcib1": {
        "class": "bridge",
        "device": "Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller",
        "subclass": "PCI-PCI",
        "vendor": "Intel Corporation"
      },
      "pcib2": {
        "class": "bridge",
        "device": "8 Series/C220 Series Chipset Family PCI Express Root Port",
        "subclass": "PCI-PCI",
        "vendor": "Intel Corporation"
      },
      "pcib3": {
        "class": "bridge",
        "device": "8 Series/C220 Series Chipset Family PCI Express Root Port",
        "subclass": "PCI-PCI",
        "vendor": "Intel Corporation"
      },
      "pcib4": {
        "class": "bridge",
        "device": "8 Series/C220 Series Chipset Family PCI Express Root Port",
        "subclass": "PCI-PCI",
        "vendor": "Intel Corporation"
      },
      "pcib5": {
        "class": "bridge",
        "device": "82801 PCI Bridge",
        "subclass": "PCI-PCI",
        "vendor": "Intel Corporation"
      },
      "re0": {
        "class": "network",
        "device": "RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller",
        "subclass": "ethernet",
        "vendor": "Realtek Semiconductor Co., Ltd."
      },
      "vgapci0": {
        "class": "display",
        "device": "GM206 [GeForce GTX 960]",
        "subclass": "VGA",
        "vendor": "NVIDIA Corporation"
      },
      "xhci0": {
        "class": "serial bus",
        "device": "8 Series/C220 Series Chipset Family USB xHCI",
        "subclass": "USB",
        "vendor": "Intel Corporation"
      }
    }
  },
  "id": "fooid",
  "name": "response",
  "namespace": "sysadm"
 }
