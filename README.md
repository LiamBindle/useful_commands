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

Add, subtract, multiply, divide operations all variables in multiple NetCDF files:
```
ncbo --op_typ=add 1.nc 2.nc 3.nc
```

Compress NetCDF file:
```
nccopy -d1 test.nc testd1.nc
```

Keep variables with names matching a regex:
```
  ncks -v foo in.nc out.nc
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

### Misc

Run a command in each directory with a file:
```
find -name conf.yml -execdir python -m cog.fill \;
```
