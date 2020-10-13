### File transfer

Local file transfer:
```
rsync -avAXEWSlHRh /./ExtData . --no-compress --info=progress2
```

### NetCDF

Change attribute inplace:
```
ncatted -O -h -a units,time,o,c,'hours since 1985-1-1 00:00:00' inout.nc
```

Add, subtract, multiply, divide operations on variables in a single NetCDF file:
```
ncap2 -s 'var3=(var1+var2)' in.nc out.nc
```

Note: max chunk size if 4GB. Use the `--cnk_dmn time,50` option to chunk the dataset <4GB.

Add, subtract, multiply, divide operations all variables in multiple NetCDF files:
```
ncbo --op_typ=add 1.nc 2.nc 3.nc
```

Compress NetCDF file (this is usually extremely slow):
```
nccopy -d1 test.nc testd1.nc
```

Keep variables with names matching a regex:
```
  ncks -v foo in.nc out.nc
```

Concatenate files together
```
ncrcat GCHP.MassCons.201* masscons1.nc
```

### Video creation

Convert jpegs to mp4:
```
ffmpeg -framerate 24 -pattern_type glob -i '*.jpeg' -b:v 100000k -crf 1 -vf format=yuv420p  China-D2.mp4
```

Change mp4 to webm and balance quality and file size:
```
ffmpeg -i China-D2.mp4 -c:v libvpx-vp9 -b:v 2M -c:a libvorbis China-D2-MR.webm
```

Convert webm to mp4 (for PPT etc):
```
ffmpeg -i Stretch-MR.webm Stretching-Demo.mp4
```

### Image manipulation
Create a grid of images
```
montage -geometry +1+1 -tile 4x1 EU*/rvd-O3.png montage_rvd-EU.png
```

Vertically stack and left align images
```
convert montage_rvd-EU.png montage_rvd-IN.png -gravity West -append out.png
```

### Misc

Run a command in each directory with a file:
```
find -name conf.yml -execdir python -m cog.fill \;
```

Launch LSF job for each directory with a file:
```
find sg-ensemble-2/c180e -name 'conf.yml' -execdir sh -c "bsub < /home/IDC-ID-74944/scratch1/liam.bindle/iwa.bsub" \;
```
