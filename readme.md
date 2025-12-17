# abcde Configuration File

My custom .conf files for abcde CD ripper.

**Conventions:**

- Path to file should be commented at the top of the file.
- Any aliases related to the application should be commented at the top of the file.

## Basic Settings
.abcde.conf
- includes cue sheet
- compression level 5
- embeds album art
- verbosity level 2
- accepts first available option and does not prompt user
- cddb: http://gnudb.gnudb.org/
  



**abcde CD ripper**

[abcde page](https://abcde.einval.com/wiki/)

[abcde man page](https://linux.die.net/man/1/abcde)

config file: [.abcde.conf](.abcde.conf)




### For Multi-Disc Sets
There does not appear to be a way to rip these into a unified set of files with
the .conf file. They must be done via command line arguments. I haven't found a
way to do this using the -1 (make one track) argument. So far it only works if
you make a separate flac file for each song.

Rip discs sequentially like this:

**Disc 1**
```shell
abcde -W 1
```

**Disc 2**
```shell
abcde -W 2
```

**Disc 3**
```shell
abcde -W 3
```


This places all tracks in the same album directory (using existing OUTPUTFORMAT), with continuous/offset numbering for easy merging later.



**Notes:**
The emoticons in the terminal window are not random. They are status messages from cdparanoia
See [CD Paranoia man page](https://linux.die.net/man/1/cdparanoia)

To change settings not covered in abcde docs, change the arguments to the programs it uses by
setting `COMMAND-LINE OPTIONS` in the .conf file.

Relevant man pages:
- [CD Paranoia](https://linux.die.net/man/1/cdparanoia): Reads the CD
- [Icedax](https://linux.die.net/man/1/icedax): Writes the .wav file (mono vs stereo settings)
-(cdda2wav(1))[https://linux.die.net/man/1/cdda2wav]: Writes the .wav file
