# DQM-Integration

Repository to store input files for the CMSSW [DQM/Integration](https://github.com/cms-sw/cmssw/tree/master/DQM/Integration) package.

## Streamer Files
For the moment this repository is used to store streamer files that are needed as input for the unitTest.

Currently the unitTest that make use of input streamer files are:
   * the `beamhlt_dqm_sourceclient-live_cfg` client, it reads the `streamDQMOnlineBeamspot` streamer files that are from run 356383 ([OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=356383&cms_run_sequence=GLOBAL-RUN)):
```
run356383_ls0010_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
run356383_ls0010_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
run356383_ls0020_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
run356383_ls0020_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
```
   * the `ecalgpu_dqm_sourceclient-live_cfg.py`, `hcalgpu_dqm_sourceclient-live_cfg.py` and `pixelgpu_dqm_sourceclient-live_cfg.py` read the `streamDQMGPUvsCPU` streamer files that are from run 369956 ([OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=369956&cms_run_sequence=GLOBAL-RUN)):
```
run369956_ls0001_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0001_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0002_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0002_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0003_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0003_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0004_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0004_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0005_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0005_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0006_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0006_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0007_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0007_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0008_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0008_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0009_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0009_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0011_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0011_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0012_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0012_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0013_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0013_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0014_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0014_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0015_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0015_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0016_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0016_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0017_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0017_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0018_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0018_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
run369956_ls0019_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
run369956_ls0019_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
```

## Possible extenstions

There are two more clients for which the unitTets could be activated in the future, namely:
```
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-ecalcalib_dqm_sourceclient" command="runtest.sh ecalcalib_dqm_sourceclient-live_cfg.py" /> -->
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-hcalcalib_dqm_sourceclient" command="runtest.sh hcalcalib_dqm_sourceclient-live_cfg.py" /> -->
```
