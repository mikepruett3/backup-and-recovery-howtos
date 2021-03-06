# Recovery w/ MergerFS & CrashPlan

This assumes a setup similar to what is described [here](backup_(mergerfs,crashplan).md).

### Full drive recovery

#### Initial state

* 4 Pooled Drives
  * /mnt/data0
  * /mnt/data1
  * /mnt/data2
  * /mnt/data3
* Pool mountpoint: /mnt/pool
* Failed drive: /mnt/data1
* New drive: /mnt/data4

#### Restore Procedure

1. Remove failed drive from mergerfs pool  
`$ sudo xattr -w user.mergerfs.srcmounts -/mnt/data1 /mnt/pool/.mergerfs`
2. [Format disk4](backup_(mergerfs,crashplan).md#1-format-the-drives)
3. Add `data4` to fstab
4. Mount  
`$ sudo mount /mnt/data4`
5. Add new drive to mergerfs pool  
`$ sudo xattr -w user.mergerfs.srcmounts +/mnt/data4 /mnt/pool/.mergerfs`
6. Open the CrashPlan GUI
7. Select Restore from the left panel
8. Click on `most recent` and change the date/time to be before the drive died
8. Navigate in the file viewer to `/mnt/data1` and select the directory
9. Click `Desktop` till `a folder (Desktop)` appears. Click on `(Desktop)` and select `/mnt/data4`
10. Click `Restore`
11. Wait for CrashPlan to restore all files
