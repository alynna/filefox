# Filefox

filefox: The fastest way to get from here to there.

Version v1.3; (C) 2018 Alynna Trypnotk; GPL3

Sick of slow transfers using rsync or copying over the network?

Do you wish there was just a way to get your files from here to there?

Try this.

Features:
* Resumable file transfers (Will check what files are already present, or you can restart from scratch)
* Fast file selection (Sends a list of what's already on the remote host and excludes them from the copy)
* RSYNC based file selection (Will sync what rsync says needs to be synced, but do the sync in filefox.  Slowest to get started to copy.)
* Progress readout while copying.
* lzop -1 compression as default, fast enough to keep your network saturated.  Won't slow you down.
* LZOP not doing it for you?  Swap the compressor with any other stream based compressor (must take data from stdin, send out stdout, and take the -d option to decompress.  Almost all compression programs do this.)
* Sets up over SSH, copies over faster unencrypted socket.
* Change sizes of blocks, buffers and timeouts, and save the defaults to the script.

```
 Syntax:
  filefox [options] <user@host> <local-dir> <remote-dir>
 Options:
  -n; --new             Start transfer fresh without finding out what files exist in the destination.
                        Best for starting a new transfer.
  -f; --fast            Scan the destination for the existence of files only, does not compare times
                        or file sizes.  (DEFAULT)
  -r; --rsync           Uses rsync to determine which files should be copied, then copies them using
                        filefox.  Can catch files that didn't transfer properly that --fast doesn't
                        catch.
  -r=<opts>
  -rsync=<opts>         Adds additional options to rsync when doing an "rsync" bbased transfer.
  --compressor="<prog>[ opts]"
  -c="<prog>[ opts]"    Uses a different compressor than the default "lzop -1".
                        This can be any stream based compressor on your system that uses the -d option
                        to specify decompression.
  -k; --privatekey      Do not ask for an SSH password at the beginning, assume private key present.
  -w; --password        Ask for an ssh password and attempt to use it via SSHPASS.  (DEFAULT)
  -q; --prerequisites   Install prerequisite programs.  Works on debian based systems.  For other
  -p=<port>             Connect on different port
  --port=<port>          Default port: 65432
  -s=<blocksize>        Set blocksize of TAR records and socat transfer size
  --blocksize=<port>     Default blocksize: 65536
  -b=<bufsize>          Total TCP buffer size
  --buffer=<bufsize>     Default buffer size: 16777216
  -t=<secs>             Total inactivity tolerance
  --timeout=<port>       Default inactivity tolerance: 60```
