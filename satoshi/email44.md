Date: Tue, 27 Oct 2009 04:45:47 +0000
From: Satoshi Nakamoto <satoshin@gmx.com>
To: mmalmi@cc.hut.fi
Subject: Re: Fw: bitcoin.sourceforge.net

* | Bitweaver,
  * users can edit (delete, ..) their own messages | forum?

* | be portable to Linux
  * -> 
    * double testing & building workload
    * better approach: use standard C stuff (instead of Windows calls)

* Threading API 
  * NOT portable BETWEEN Windows -- & -- Unix
    * ways
      * MSVC's `_beginthread`
        * ONLY AVAILABLE | Windows 
          * == NOT AVAILABLE | C library
      * wxWidgets's `wxCriticalSection`
    * Reason: Windows did NOT copy Unix one 

* Sockets API
  * portable BETWEEN Windows -- & -- Unix
    * Reason: Winsock copied -- from -- Unix BSD Sockets
  * recommendation
    * direct control 
      * == low level layers
      * != abstraction layers (== high level layers) 

* wxWidgets
  * uses
    * look for cross-platform support functions

* code style
  * avoid `#ifdef`
    * if you need -> create a function | "util.cpp"

* Problems:
  * | uninstall Bitcoin,
    * NOT remove Bitcoin autostart icon
