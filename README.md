# DQM-Integration

Repository to store input files for the CMSSW [DQM/Integration](https://github.com/cms-sw/cmssw/tree/master/DQM/Integration) package.

## Streamer Files
For the moment this repository is used to store streamer files that are needed as input for the unitTest.

Currently only one unitTest is for the `beamhlt_dqm_sourceclient-live_cfg` client, it reads the `streamDQMOnlineBeamspot` stream files that are from run 346373 ([OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=346373&cms_run_sequence=GLOBAL-RUN)):
```
DQM-Integration/run346373/run346373_ls0027_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
DQM-Integration/run346373/run346373_ls0027_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
DQM-Integration/run346373/run346373_ls0028_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
DQM-Integration/run346373/run346373_ls0028_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
DQM-Integration/run346373/run346373_ls0029_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
DQM-Integration/run346373/run346373_ls0029_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
```
There are two more clients for which the unitTets could be activated in the future, namely:
```
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-ecalcalib_dqm_sourceclient" command="runtest.sh ecalcalib_dqm_sourceclient-live_cfg.py" /> -->
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-hcalcalib_dqm_sourceclient" command="runtest.sh hcalcalib_dqm_sourceclient-live_cfg.py" /> -->
```
