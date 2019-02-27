# amdgpu-utils
A set of utilities for monitoring AMD GPU performances and modifying control settings.

In order to use any of these utilities, you must have the *amdgpu* open source driver
package installed. You also must first set your linux machine to boot with
amdgpu.ppfeaturemask=0xffff7fff.  This can be accomplished by adding
amdgpu.ppfeaturemask=0xffff7fff to the GRUB_CMDLINE_LINUX_DEFAULT value in 
/etc/default/grub and executing *sudo update-grub*

## amdgpu-ls
This utility displays most relevant parameters for installed and compatible AMD GPUs.
The default behavior is to list relevant parameters by GPU.  OpenCL platform information
is added when the *--clinfo* option is used.  The *--no_fan* can be used to ignore fan
settings.  The *--pstate* option can be used to output the p-state table for each GPU
instead of the list of basic parameters.  The *--ppm* option is used to output the table
of available power/performance modes instead of basic parameters.

## amdgpu-monitor
A utility to give the current state of all compatible AMD GPUs. The default behavior
is to continuously update a text based table in the current window unitl Ctrl-C is
pressed.  With the *--gui* option, a table of relevant parameters will be updated
in a Gtk window.  You can specify the delay between updates with the *--sleep N*
option where N is an integer > zero that specifies the number of seconds to sleep.
The *--no_fan* option can be used to disable the reading and display of fan
information.

## amdgpu-pac
Program and Control compatible AMD GPUs with this utility.  By default, the commands to
be written to a GPU are written to a bash file for the user to inspect and run.  If you
have confidence, the *--execute_pac* option can be used to execute the bash file when saved
and then delete it. Since the GPU device files are writable only by root, sudo is used to
execute commands in the bash file, as a result, you will be prompted for credentials in the
terminal where you executed *amdgpu-pac*. The *--no_fan* option can be used to eliminate
fan details from the utility.

## New in this Release  -  v2.1.0
* Significant bug fixes and error proofing.  Added messages to stderr for missing driver related files.
* Added fan monitor and control features.
* Implemented --no_fan option across all tools.  This eliminates the reading and display of fan parameters and useful for those who have installed GPU waterblocks.
* Implemented P-state masking, which limits available P-states to those specified. Useful for power management.
* Fixed implementation of global variables that broke with implementation of modules in library.
* Added more validation checks before writing parameters to cards.

## New in Previous Release  -  v2.0.0
* Many bug fixes!
* First release of amdgpu-pac.
* Add check of amdgpu driver in the check of environment for all utilities.  Add display of amdgpu driver version.
* Split list functions of the original amdgpu-monitor into amdgpu-ls.
* Added --clinfo option to amdgpu-ls which will list openCL platform details for each GPU.
* Added --ppm option to amdgpu-ls which will display the table of available power/performance modes available for each GPU.
* Error messages are now output to stderr instead stdout.
* Added power cap and power/performance mode to the monitor utilities.  I have also included them in the amdgpu-ls display in addtion to the power cap limits.

## New in Previous Release  -  v1.1.0
* Added --pstates feature to display table of p-states instead of GPU details.
* Added more error checking and exit if no compatible AMD GPUs are found.

## New in Previous Release  -  v1.0.0
* Completed implementation of the GPU Monitor tool.

## Development Plans
* Write a users guide.
* Enhance formatting in Gtk monitor tool. Need to improve my Gtk skills!
* Develop a startup utility to initialize GPU settings at boot up.
* Include most detailed GPU name in reading from lspci and amdgpu-ls output. Optimize both long and short names.
* Implement an option to only write changes in amdgpu-pac.
* Implement logging option for amdgpu-monitor.
* Implement energy meter.
* Implement card level compatibility flagging and use in showing only compatible cards.

## References
* Original inspiration for this project: <a href="https://www.reddit.com/r/Amd/comments/agwroj/how_to_overclock_your_amd_gpu_on_linux/?st=JSL25OVP&sh=306c2d15">Reddit</a>
* Phoronix articles including these: <a href="https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-Quick-WattMan-Cap-Test">Phoronix Power Cap</a>, <a href="https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-Linux-4.17-Round-1">Phoronix HWMon</a>
* Repositories: <a href="https://github.com/sibradzic/amdgpu-clocks">amdgpu-clocks</a>, <a href="https://github.com/BoukeHaarsma23/WattmanGTK">WattmanGTK</a>, <a href="https://github.com/RadeonOpenCompute/ROC-smi">ROC-smi</a>
