iohist
======

Tool to see what processes are doing IO. Akin to iotop, but with fewer
dependencies.

So, you're a sysadmin: and you know (from iostat, and whatnot) that you've got
a drive that's getting hammered.  Wouldn't it be nice to know what process is
actually hammering it?  There are things out there like iotop and what not, but
they generally rely on new kernel features, or things that are rather more
invasive.  Over the weekend, I needed something for an older kernel, and which
wouldn't be invasive.

Enter iohist (with a nice tip o' the hat to iodump).  It relies on 
'echo 1 > /proc/sys/vm/block_dump'
to do it's magic, looping over 'dmesg -c' at an
interval (currently 5 seconds).  

NOTE: this program does the 'echo 1 > /proc/sys/vm/block_dump' for you...
technically it sees if it's a zero value, overrides it if it is, and reverts
it back when you exit.

Goals:
1) a few more configuration options (like allowing a change of the interval
   from 5 seconds)
2) Maybe get more clever about translating dm-6 into 'this is your swap 
   partition'
