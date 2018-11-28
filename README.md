# check-media-integrity
##Overview
This tool automatically checks the integrity of media files (pictures, video, audio).
The tool tests if common library (Pillow, ImageMagik, FFmpeg) are effectively able to decode the media files, but **image, audio and video format are very resilient to defects and damages**.

This tool is able with 100% confidence to spot files that have broken header/metadata and truncated image files.

In the case you know ways to instruct Pillow, Wand and FFmpeg to be strcter than now when decoding, please tell me.

help message:
```usage: check_mi.py [-h] [-c X] [-v] [-r] [-i] [-m] [-p] [-e] [-x E] P

Checks integrity of Media files (Images, Video, Audio).

positional arguments:
  P                     path to the file or folder

optional arguments:
  -h, --help            show this help message and exit
  -c X, --csv X         Save bad files details on csv file X
  -v, --version         show program's version number and exit
  -r, --recurse         Recurse subdirs
  -i, --disable-images  Ignore image files
  -m, --enable-media    Ignore audio/video files
  -p, --disable-pdf     Ignore pdf files
  -e, --disable-extra   Ignore extra image extensions (psd, xcf,. and rare
                        ones)
  -x E, --err-detect E  Execute ffmpeg decoding with a specific err_detect
                        flag E, 'strict' is shortcut for
                        +crccheck+bitstream+buffer+explode

- Single file check ignores options -i,-m,-p,-e,-c

- With 'err_detect' option you can provide the strong shortcut or the flags
supported by ffmpeg, e.g.: crccheck, bitstream, buffer, explode, or their
combination, e.g., +buffer+bitstream

- Supported image formats/extensions: ['jpg', 'jpeg', 'jpe', 'png', 'bmp',
'gif', 'pcd', 'tif', 'tiff', 'j2k', 'j2p', 'j2x', 'webp']

- Supported image EXTRA formats/extensions:['eps', 'ico', 'im', 'pcx', 'ppm',
'sgi', 'spider', 'xbm', 'tga', 'psd', 'xcf']

- Supported audio/video extensions: ['avi', 'mp4', 'mov', 'mpeg', 'mpg',
'm2p', 'mkv', '3gp', 'ogg', 'flv', 'f4v', 'f4p', 'f4a', 'f4b', 'mp3', 'mp2']

- Output CSV file, has the header raw, and one line for each bad file,
providing: file name, error message, file size
```
##Examples

Check a single file:
```check_mi.py ./test_folder/files/050807-124755t.jpg```

Check a folder:
```check_mi.py ./test_folder/files```

Check a folder, and subfolder recursiverly
```check_mi.py -r ./test_folder/files```

Check a folder, and subfolder recursiverly and also check media (audio and video)
```check_mi.py -m -r ./test_folder/files```

Check a folder, and subfolder recursiverly and save bad files details to out.csv file:
```check_mi.py -r ./test_folder/files -c ./test_folder/output/out.csv```

##Test damage
test_damage.py is a funny experiment, it evaluates the probability of a random damage to be detected by this tool.
That is.. it is very low, the damage has to be in vital parts (very small portion of the file) or to be a file truncation.
I think that the code is self explanatory.