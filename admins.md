# Bletchley Administrators Guide

This guide assumes basic Linux and command line usage.

## Support Hierarchy

As of 2023-03-29, David Dellinger <mailto:ddellinger@oxy.edu>, Jeff Cannon <jcannon@oxy.edu>, and Justin Li <justinnhli@oxy.edu> are the administrators with the ability to create new users. If you would like additional permissions, or have questions about the cluster, please email all three of us.

## Adding New Users

1. Log in as root on Bletchley. In the home directory (`/root`), there is an interactive `usersetup` script. Run it with `./usersetup`.

2. Note that the new user __does not have a password__. It is highly recommended that a temporary password be created with `passwd [USERNAME]`. Afterwards, you can use `passwd --expire [USERNAME]` to force the user to set a new password when they next log in.

3. Update the Bletchley Users spreadsheet: <https://docs.google.com/spreadsheets/d/1gbY_t3s39BW124KT_ovrtSWSaCmdWHzFHq3iW_bGiHA/edit#gid=0>

## System Monitoring

Uptime, usage, and other statistics can be found on [Ganglia](https://ganglia.oxy.edu/ganglia/).

## Installing Matlab Toolboxes

Matlab toolboxes can be installed via the Matlab graphical interface, under the Environment > Add-Ons > Get Add-Ons in the ribbon. The tricky part is starting Matlab graphically _after_ `su`-ing as `root`, since Matlab requires permissions to download and save the toolboxes. The set of instructions below is adapted from <https://www.simplified.guide/ssh/x11-forwarding-as-root>:

1. `ssh -Y` to Bletchley as usual.
2. `echo $DISPLAY` to print the `DISPLAY` environment variable. The output should look something like `localhost:11.0`.
3. `xauth list $DISPLAY` to print the X authorization for that display. The output should look something like `bletchley.oxy.edu/unix:11 MIT-MAGIC-COOKIE-1 c011571d3221b13d607dd98c3f53c3d3`.
4. `su` to `root`
5. `export DISPLAY=localhost:11.0`, substituting `localhost:11.0` with the output of Step 2 above.
6. `xauth add bletchley.oxy.edu/unix:11 MIT-MAGIC-COOKIE-1 c011571d3221b13d607dd98c3f53c3d3`, substituting the last three terms with the output of Step 3 above

You should now be set for X11 port forwarding as root, and you can run `xclock` to confirm.

## Bletchley Technical Details

A total of 27 nodes are currently part of Slurm:

* the head node
* the storage node
* computer nodes `n001` to `n024`
* the GPU node `gpu1`

A list of additional nodes and their owners can be found at <https://docs.google.com/spreadsheets/d/12IxAKP-Ieh4plhyPw7QrCqftc2rbow_nuxuc_XUx4PU/edit#gid=0>

## System Test Scripts
