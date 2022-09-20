# Bletchley Administrators Guide

* assumes basic Linux and command line usage

## Adding New Users

1. As of 2021-10-19, David Dellinger <mailto:ddellinger@oxy.edu>, Jeff Cannon <jcannon@oxy.edu>, and Justin Li <justinnhli@oxy.edu> are the administrators with the ability to create new users.

2. Log in as root on Bletchley. In the home directory (`/root`), there is an interactive `usersetup` script. Run it with `./usersetup`.

3. Note that the new user __does not have a password__. It is highly recommended that a temporary password be created with `passwd [USERNAME]`. Afterwards, you can use `passwd --expire [USERNAME]` to force the user to set a new password when they next log in.

4. Update the Bletchley Users spreadsheet: <https://docs.google.com/spreadsheets/d/1gbY_t3s39BW124KT_ovrtSWSaCmdWHzFHq3iW_bGiHA/edit#gid=0>

## Support Hierarchy

* getting on the sudoers list

## Slurm Technical Details

## System Monitoring

## System Test Scripts

## Configuration Details
