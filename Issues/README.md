## Issue Summary

Did not have the correct eedata file in the run directory. This incorrect file was copied from one of the tutorial folders.

## MITgcm Message
The grid spacing error was indicated in the slurm output file. 

STOP ABNORMAL END: S/R LOAD_GRID_SPACING
STOP ABNORMAL END: S/R LOAD_GRID_SPACING
STOP ABNORMAL END: S/R LOAD_GRID_SPACING
STOP ABNORMAL END: S/R LOAD_GRID_SPACING 


## Issue Remedy

Changed  'delX = 2,
     'delY = 2,

to  `delX = 180*2,
    `delY = 90*2,
