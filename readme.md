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



**Typical Output looks like:**
```shell
# => 1 item in total.
copying cover to target directory /home/hoo/Music/flac/INXS-Live Baby Live
Grabbing tracks 01 - 16 as one track ...
cdparanoia III release 10.2 (September 11, 2008)

Ripping from sector       0 (track  0 [0:00.00])
	  to sector  287001 (track 16 [6:16.61])

outputting to /home/hoo/abcde.f20ef210/track01.wav

 (== PROGRESS == [                              | 287001 00 ] == :^D * ==)   

Done.


 echo Encoding track 01 of 01: Live Baby Live...
Encoding track 01 of 01: Live Baby Live...
encodetrack-flac-01 nice -n 10 flac -f -s -e -V -8 -o /home/hoo/abcde.f20ef210/track01.flac /home/hoo/abcde.f20ef210/track01.wav
encodetrack-01 true
 echo Tagging track 01 of 01: Live Baby Live...
Tagging track 01 of 01: Live Baby Live...
tagtrack-flac-01 nice -n 10 metaflac --no-utf8-convert --import-cuesheet-from=/home/hoo/abcde.f20ef210/cue-f20ef210.txt --import-tags-from=- /home/hoo/abcde.f20ef210/track01.flac
tagtrack-01 true
Adding metadata to the cue file...
movetrack-01 mv /home/hoo/abcde.f20ef210/track01.flac /home/hoo/Music/flac/INXS-Live Baby Live/Live Baby Live.flac
movetrack-output-flac true
movecue-flac cp /home/hoo/abcde.f20ef210/cue-f20ef210.txt /home/hoo/Music/flac/INXS-Live Baby Live/Live Baby Live.flac.cue
Successfully embedded the album art into your flac tracks
Finished.

```



**Troubleshooting:**
**Flashing Done**
If it's flashing "Done" and doesn't immediately move to the Encoding cycle, it's hung. Hit Ctrl-C and start over.


**No album art**
It means the selected CDDB list didn't have the art. 
Disable non-interactive mode in the conf file and choose another data set.

