# pb_chime5: Front-End Processing for the CHiME-5 Dinner Party Scenario [\[pdf\]](http://spandh.dcs.shef.ac.uk/chime_workshop/papers/CHiME_2018_paper_boeddecker.pdf)

This repository includes all components of the CHiME-5 front-end presented by Paderborn University on the CHiME-5 workshop [PB2018CHiME5].
In combination with an acoustic model presented by the RWTH Aachen this multi-array front-end achieved the third best results during the challenge with 54.56 %. 

The front-end consists out of WPE, a spacial mixture model that uses time annotations (GSS), beamforming and masking:

![(System Overview)](doc/images/system.svg)

The core code is located in the file `pb_chime5/core.py`.
An example script to run the enhancement is in `pb_chime5/scripts/run.py` and can be executed with `python -m pb_chime5.scripts.run with session_id=dev wpe=True wpe_tabs=2`.

Challenge website: http://spandh.dcs.shef.ac.uk/chime_challenge/

Workshop website: http://spandh.dcs.shef.ac.uk/chime_workshop/

If you are using this code please cite the following paper:

```
@Article{PB2018CHiME5,
  author    = {Boeddeker, Christoph and Heitkaemper, Jens and Schmalenstroeer, Joerg and Drude, Lukas and Heymann, Jahn and Haeb-Umbach, Reinhold},
  title     = {{Front-End Processing for the CHiME-5 Dinner Party Scenario}},
  year      = {2018},
  booktitle = {CHiME5 Workshop},
}
```

ToDos:

- [x] core enhancement code
- [x] remove dependencies from our infrastructure
- [x] launch script
- [x] manual script
- [ ] code cleanup, remove all unnessesary code and rearrange the code files

## Installation

Does not work with Windows.

Clone the repo with submodules
```bash
$ git clone https://github.com/fgnt/pb_chime5.git
$ cd pb_chime5
$ # Download submodule dependencies  # https://stackoverflow.com/a/3796947/5766934
$ git submodule init  
$ git submodule update
```
Create a symlink to the chime5 database e.g. `ln -s /net/fastdb/chime5/CHiME5 CHiME5`

Install this package, toolbox and pb_bss 
```bash
$ pip install --user -e pb_bss/
$ pip install --user -e toolbox/  # Copy of some internal developed code.
$ pip install --user -e .
```

Create the database description file
```bash
$ make cache/chime5_orig.json
```

It is assumed that the folder `sacred` in this git is the simulation folder.
If you want to change the simulation dir, add a symlink to the folder where you want to store the simulation results: `ln -s /path/to/sim/dir sacred`

Start a testrun with
```bash
$ python -m pb_chime5.scripts.run test_run with session_id=dev
```

Start a simulation with 9 mpi workers (1 scheduler and 8 actual worker)
```bash
$ mpiexec -np 9 python -m pb_chime5.scripts.run with session_id=dev
```
You can replace `mpiexec -np 9` with your HPC command to start a MPI program.
It scalles up very well and is tested with 600 distributed cores.




