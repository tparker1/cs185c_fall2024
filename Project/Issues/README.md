## Issue Summary

In my run/data file, I did not correctly specify my delX and delY parameters. 

## MITgcm Message

The grid spacing error was indicated in the slurm output file. 

`STOP ABNORMAL END: S/R LOAD_GRID_SPACING`

`STOP ABNORMAL END: S/R LOAD_GRID_SPACING`

`STOP ABNORMAL END: S/R LOAD_GRID_SPACING`

`STOP ABNORMAL END: S/R LOAD_GRID_SPACING` 


## Issue Remedy

In the run/data file, I changed:

     `delX = 2,`
     `delY = 2,`

to  

     `delX = 180*2,`
     `delY = 90*2,`
