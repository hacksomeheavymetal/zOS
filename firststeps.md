# z/OS booting, logging and working environments

## Setting up [hercules](http://www.hercules-390.org/):

Download, install/compile and run hercules as an administrator/root:

- Connect two instances of x3270 terminals to IP with hercules running (port and number of console devices are defined in the hercules config file). For special/function keys it's best to use virtual keyboard of the terminal's emulator, e.g. attention keys, function keys (especially on Mac OSX) etc. 

- Press escape to switch to hercules curses view. Press 'l' and type in the number of the first DASD (disk) device. Alternatively you can type in the cli view the ipl command with the number of the first DASD:

  `ipl 0xXXX`

- If the "cpumodel" in hercules config file is changed from 2084 (z990 series, mfg2003) to 2827 (zEnterprise EC12, mfg2012), then it's not required to enter commands below. Otherwise type in the following commands when prompted on the master console:

  `r 00,r`
  
  `r 00,couple=**`

## Logging in:

The z/OS system should be now booted/IPLed. You should notice that the second x3270 terminal displays login/welcome screen.

- On the login screen enter credentials, e.g.:

  `login: ibmuser`
  
  `pass: sys1`
  
  `proc: ISPFPROC|OMVSPROC|IKJACCNT`

- On the welcome screen enter userid and see 2.1., e.g.:

  `logon ibmuser`

## Working envrionments:

Depending on the chosen procedure you will end up in on of the working environments.

- ISPF:

  Courses-like environment with various panels. Allows to perform various tasks on its own, execute commands in TSO, run installed utilities in the z/OS etc.

- OMVS:

  Also known as Unix System Services is a POSIX compliant unix that runs within the z/OS itself. Similar to other unices. Execute "omvs" in TSO  (may not work if you don't have a pseudo terminal allocated, e.g. via SSH. In such case remove and create symlink in / to dev).

- TSO:

  Time Sharing Option is like a login session on linux. Very basic. You can run various commands and applications including "omvs" and "ispf". By typing "ishell" you can run ISPF shell that allows you to run commands in the OMVS.

## Basic navigation:

In the ISPF-like programs:

  - PF10/PF11 shifts screen view right/left to see all displayed info
  
  - PF7/PF8 scrolls screen view up/down to see all displayed info
  
  - PA1 attention key on the virtual keyboard that terminates the execution of the current command in TSO (e.g. when in the '***' prompt).
  
  - use "File -> Save screen contents" in x3270 (or similar) to save output from the terminal to a local file
  
  - you can abbreviate some of the commands, e.g. setropts -> setr, listcat -> listc etc.

## Cool! What else?

For other basic information on mainframe and z/OS watch the IBM introductionary course: https://www.youtube.com/watch?v=NIboxgbQaqE
