# Filefox
''''
The fastest way to get your data from here to there.

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
  -p=<port>
  --port=<port>         Connect on different port (DEFAULT=65432)"
  -q; --prerequisites   Install prerequisite programs.  Works on debian based systems.  For other
                        systems, these are expected:  rsync, pv, lzop, ssh, sshpass
''''
