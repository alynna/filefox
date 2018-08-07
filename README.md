# Filefox

filefox: The fastest way to get from here to there.

Sick of slow transfers using rsync or copying over the network?  Do you wish there was just a way to get your files from here to there?  Try this.

Features:
* Defaults can be changed at the top of the script and overriden anytime with options.
* Resumable file transfers (Will check what files are already present, or you can restart from scratch)
* Fast file selection (Sends a list of what's already on the remote host and excludes them from the copy)
* Progress readout while copying.  Shows both how much data is transferred and how much is going over the connection.
* lzop -1 compression as default, fast enough to keep your network saturated.  Won't slow you down.
* LZOP not doing it for you?  Swap the compressor with any other stream based compressor (must take data from stdin, send out stdout, and take the -d option to decompress.  Almost all compression programs do this.)
* IPv6 friendly.
* Supports any transport 'socat' has a -listen directive for.  Try SCTP for example.
* Sets up over SSH, copies over faster unencrypted socket.
* * OpenSSL encryption over the link can be enabled.
* Change sizes of blocks and buffers, and save the defaults to the script.
* Uses rsync to verify the transfer and 'catch it up' afterwords.

Bugs:
* Due to the way tar handles its 'exclude-from' contents, some filenames with wildcards may be unconditionally re-transferred.

Help output:
```
filefox: The fastest way to get from here to there.
Version 3.5 (C) 2018 Alynna Trypnotk; GPL3
 Syntax:
  filefox [options] <user@host> <local-dir> <remote-dir>
 Options:
  -n; --new             Start transfer fresh without finding out what files exist in the destination.
                        Best for starting a new transfer.
  -r; --resume          (DEFAULT) Scan the destination for the existence of files and skip them.
                        WARNING: does not compare times, file sizes, or file integrity.
  -v; --verify          (DEFAULT) Check the copy with rsync after doing the copy.  This occurs at the
                        end and is a good compromise between filefox's speed and rsync's reliability.
  -v0; --no-verify      Skip rsync verification check after copy.
  -y; --encrypt         Pipe through OpenSSL encryption (Slower)
  -y0; --no-encrypt     (DEFAULT) Do not encrypt (Fast)
  --compressor="<prog>" Uses a different compressor than the default "lzop -1".
  -c="<prog>"           This can be any stream based compressor on your system that uses the -d option
                        to specify decompression.
  -k; --privatekey      Do not ask for an SSH password at the beginning, assume private key present.
  -w; --password        (DEFAULT) Ask for an ssh password and attempt to use it via SSHPASS.
  -q; --prerequisites   Install prerequisite programs.  Works on debian based systems.  For other
  -t=<port>             Connect using different transport protocol, such as SCTP or UDP
  --transport=<tport>    Default transport: tcp
  -p=<port>             Connect on different port
  --port=<port>          Default port: 65432
  -l=<bytespec>         Limit bandwidth to <bytes>, K M G T can be used
  --limit=<bytespec>     Default limit: 0
  -s=<blocksize>        Set blocksize of TAR records and socat transfer size
  --blocksize=<port>     Default blocksize: 65536
  -b=<bufsize>          Total TCP buffer size
  --buffer=<bufsize>     Default buffer size: 1048576
```
