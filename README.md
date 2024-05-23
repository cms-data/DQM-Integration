# DQM-Integration

Repository to store input files for the CMSSW [DQM/Integration](https://github.com/cms-sw/cmssw/tree/master/DQM/Integration) package.

## Streamer Files
For the moment this repository is used to store streamer files that are needed as input for the unitTest.

Currently the unitTest that make use of input streamer files are:
* the `beamhlt_dqm_sourceclient-live_cfg` client, it reads the `streamDQMOnlineBeamspot` streamer files that are from run 370580 (from 2023 pp run [OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=370580&cms_run_sequence=GLOBAL-RUN)):
   ```
   run370580/run370580_ls0503_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
   run370580/run370580_ls0503_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
   run370580/run370580_ls0504_streamDQMOnlineBeamspot_sm-c2a11-43-01.dat
   run370580/run370580_ls0504_streamDQMOnlineBeamspot_sm-c2a11-43-01.jsn
   ```

   * an older run (356383) is also available, but it's missing the information from FED 1022, as detailed in [DQM-Integration/Issues#3](https://github.com/cms-data/DQM-Integration/issues/3)
* the `ecalgpu_dqm_sourceclient-live_cfg.py`, `hcalgpu_dqm_sourceclient-live_cfg.py` and `pixelgpu_dqm_sourceclient-live_cfg.py` read the `streamDQMGPUvsCPU` streamer files that are from run 380649 (from Run2024D pp run [OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=380649&cms_run_sequence=GLOBAL-RUN)):
   ```
   run380649_ls0522_streamDQMGPUvsCPU_sm-c2a11-43-01.dat
   run380649_ls0522_streamDQMGPUvsCPU_sm-c2a11-43-01.jsn
   ```
* the `sistrip_approx_dqm_sourceclient-live_cfg.py` reads the `streamDQM` streamer files that are from run 362321 (from 2022 HI run, [OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=362321&cms_run_sequence=GLOBAL-RUN), though they have been re-HLT'ed, see for more details at [CMSHLT-2884](https://its.cern.ch/jira/browse/CMSHLT-2884)):
   ```
   run362321_ls0231_streamDQM_pid738580_sm-c2a11-43-01.dat
   run362321_ls0231_streamDQM_pid738580_sm-c2a11-43-01.jsn
   ```

## Possible extenstions

There are two more clients for which the unitTets could be activated in the future, namely:
```
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-ecalcalib_dqm_sourceclient" command="runtest.sh ecalcalib_dqm_sourceclient-live_cfg.py" /> -->
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-hcalcalib_dqm_sourceclient" command="runtest.sh hcalcalib_dqm_sourceclient-live_cfg.py" /> -->
```
