# Running Gaussian on cruntch4

Cruntch4 is the high-performance cluster run by Center for Advanced Scientific Computing and Modeling (CASCaM) and UNT Chemistry department. Here we show how we can run Gaussian jobs on cruntch4. Cruntch4 has a Linux-based system and uses [slurm](https://slurm.schedmd.com/quickstart.html) to manage the submission of calculations of jobs. 

## Connecting to cruntch4

We connect to cruntch4 using an ssh client in a terminal window. On Windows, you can use the terminal [MobaXterm](https://mobaxterm.mobatek.net), which is the terminal installed on the workstations in CCIL, and you can download it onto your laptop. MacOS has a built-in [terminal](https://support.apple.com/guide/terminal/welcome/mac), but I recommend using the [iTerm2](https://iterm2.com/) instead.

Once you have started a terminal, you will use `ssh` to log onto cruntch4:
```
ssh <USERNAME>@cruntch4.chem.unt.edu
```
where `<USERNAME>` is the user name you were given in class. 

If you are logging on for the first time, you must change the password by using `passwd` command. 

Note: you can only connect to cruntch4 if you are on the UNT network, so the above command will only work if you located on campus or are using [VPN](https://itservices.cas.unt.edu/services/accounts-servers/articles/cisco-anyconnect-mobility-client-vpn) to connect to the UNT network. 

## Home folder and basic commands 

When you log on to cruntch4, you will faced with a bash shell and located in your home folder that has the path `/home/<USERNAME>`. 

Some basic commands: 
- `pwd` - to see the path to the current folder.
- `ls` - see the files and folder in the current folder.
- `ll` - see the files and folder in the current folder with more information.
- `mkdir <FOLDER NAME>` - create a new folder/directory.
- `cd <FOLDER NAME>` - move to a given folder.
- `cd ..` - move up to the previous folder.
- `cd <PATH>` - move to a given path (e.g. `cd /home/compchem1`)/
- `cd` - move to the home folder.
- `cp <FILENAME> <NEW FILENAME>` - to copy a file to another.
- `cp -r <FOLDER> <NEW FOLDER>` - to copy a folder to another.
- `mv <FILENAME> <NEW FILENAME>` - move/rename a file/folder.

Note: please do not use spaces in file and folder names.

## Editing files

To edit files, you need to use a terminal editor such as vim that is started by using the command `vi`. 

- vi has two modes, command mode and insert mode.
- To enter insert mode, you type `i`, and then you can type and paste.
- To escape the insert mode, you use the `ESC` button.
- While in the command mode, you can enter the command panel by using `:`, and use the following 
  - `:w` - save file
  - `:wq` - save and quit
  - `:q` - quit 
  - `:q!` - quit without saving
- While in command mode, you can use the following commands to copy, cut, and paste from an internal vi buffer
  - `yy` yank (copy) line to buffer
  - `dd` delete (cut) line to buffer
  - `p` paste from buffer


This [vi cheat sheet](https://www.atmos.albany.edu/daes/atmclasses/atm350/vi_cheat_sheet.pdf) will come in handy. 

## Folder structure for Gaussian runs

You should create a new folder called `gaussian-runs` to keep all Gaussian runs for the course. You should also create a sub-folder in that folder for each lecture, system, or project, as you see relevant and helpful to keep an organized structure. 

## Submitting Gaussian jobs

To submit a Gaussian input file for calculation, we need to use a slurm submission file. 

You can copy such a submission file to the current folder by using the following command:
```
cp /storage/nas_scr/shared/groups/compchem-chem5600/gaussian-files/gaussian-g16.sub . 
```

In that file, you need to give the filename of the Gaussian input file in the current part of the submission file:
```
# Here you should specfiy the name of
# the Gaussian input file that are run.
# You can specify more than one file and
# they will then be run in batch.
Jobs="
<FILENAME>.gjf
"
```

Then you can submit the calculation by using the `sbatch` command 
```
sbatch gaussian-g16.sub
```

You can monitor the job by using the `squeue` command 

## Tasks 

- Download the [`Tyrosine_b3lyp_cc-pvdz_opt.gjf`](https://github.com/valsson-group/UNT-Chem5660-Fall2023/blob/main/Gaussian-on-cruntch4/Tyrosine_b3lyp_cc-pvdz_opt.gjf) file onto your workstation and upload it to a cruntch4 using MobaXterm.
- Submit this file for calculation.
- Download the output files to your workstations and look at the HOMO and LUMO using GaussView.
- Now do a calculation for L-Tryptophan where you should get the initial coordinates by using a smiles string from Pubchem. Here you need to copy and edit the previously used input file. 
