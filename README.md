# DQM-Integration

Repository to store input files for the CMSSW [DQM/Integration](https://github.com/cms-sw/cmssw/tree/master/DQM/Integration) package.

## Streamer Files
For the moment this repository is used to store streamer files that are needed as input for the unitTest.

Currently the unitTest that make use of input streamer files are:
* the `beamhlt_dqm_sourceclient-live_cfg.py` client, it reads the `streamDQMOnlineBeamspot` streamer files regenerated from run 381594 (from 2024E pp run [OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=381594&cms_run_sequence=GLOBAL-RUN)):
   ```
   run381594_ls1000_streamDQMOnlineBeamspot_pid1752643.dat
   run381594_ls1000_streamDQMOnlineBeamspot_pid1752643.jsn
   ```
* the `ecalgpu_dqm_sourceclient-live_cfg.py`, `hcalgpu_dqm_sourceclient-live_cfg.py`, `pixelgpu_dqm_sourceclient-live_cfg.py` and `pfgpu_dqm_sourceclient-live_cfg.py` read the `streamDQMGPUvsCPU` streamer files regenerated from run  381594 (from Run2024E pp run [OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=381594&cms_run_sequence=GLOBAL-RUN)):
   ```
  run381594/run381594_ls1000_streamDQMGPUvsCPU_pid1801423.dat
  run381594/run381594_ls1000_streamDQMGPUvsCPU_pid1801423.jsn
   ```
* the `sistrip_approx_dqm_sourceclient-live_cfg.py` reads the `streamDQM` streamer files regenerated from run 362321 (from 2022 HI run, [OMS link](https://cmsoms.cern.ch/cms/runs/report?cms_run=362321&cms_run_sequence=GLOBAL-RUN), though they have been re-HLT'ed, see for more details at [CMSHLT-2884](https://its.cern.ch/jira/browse/CMSHLT-2884)):
   ```
   run362321/run362321_ls0231_streamHIDQM_pid1816953.dat
   run362321/run362321_ls0231_streamHIDQM_pid1816953.jsn
   ```

## Recipe to regenerate Streamer files (when streamer layout gets broken)

In repsonse to issue https://github.com/cms-sw/cmssw/issues/45224, streamer files have been regenerated in a release that contains https://github.com/cms-sw/cmssw/pull/44978 (in this case `CMSSW_14_0_9_MULTIARCHS`.
This was done using the following script for the pp data:

```bash
#!/bin/bash -ex

RUNNUMBER=381594
LUMISECTION=1000

# cmsrel CMSSW_14_0_9_MULTIARCHS
# cd CMSSW_14_0_9_MULTIARCHS/src
# cmsenv
# scram b

INPUTFILE=root://eoscms.cern.ch//store/express/Run2024E/ExpressPhysics/FEVT/Express-v1/000/381/594/00000/1e2c895f-a250-45be-a7ff-ee95e636a6e9.root
rm -rf run${RUNNUMBER}*

# run on 300 events of LS 1000, with 300 events per input file
convertToRaw -f 300 -l 300 -r ${RUNNUMBER}:${LUMISECTION} -o . -- "${INPUTFILE}"

tmpfile=$(mktemp)
hltConfigFromDB --runNumber "${RUNNUMBER}" > "${tmpfile}"
cat <<@EOF >> "${tmpfile}"
process.load("run${RUNNUMBER}_cff")
process.hltOnlineBeamSpotESProducer.timeThreshold = int(1e6)

# to run without any HLT prescales
del process.PrescaleService
del process.MessageLogger
process.load('FWCore.MessageLogger.MessageLogger_cfi')

process.options.numberOfThreads = 32
process.options.numberOfStreams = 32

process.options.wantSummary = True
# # to run using the same HLT prescales as used online in LS 1000
# process.PrescaleService.forceDefault = True
@EOF
edmConfigDump "${tmpfile}" > hlt.py

cmsRun hlt.py &> hlt.log
```

While the following script for the HIon data:
```bash
#!/bin/bash -ex

# cmsrel CMSSW_14_0_9_MULTIARCHS
# cd CMSSW_14_0_9_MULTIARCHS/src
# cmsenv
# scram b

# run 362321, LSs 231-232
INPUTFILE=root://eoscms.cern.ch//eos/cms/store/user/cmsbuild//store/hidata/HIRun2022A/HITestRaw0/RAW/v1/000/362/321/00000/f467ee64-fc64-47a6-9d8a-7ca73ebca2bd.root

HLTMENU=/dev/CMSSW_14_0_0/HIon/V141

rm -rf run362321*

# run on 100 events of LS 231, with 100 events per input file
convertToRaw -f 100 -l 100 -r 362321:231 -s rawDataRepacker -o . -- "${INPUTFILE}"

tmpfile=$(mktemp)
hltConfigFromDB --configName "${HLTMENU}" > "${tmpfile}"
sed -i 's|process = cms.Process( "HLT" )|from Configuration.Eras.Era_Run3_cff import Run3\nprocess = cms.Process( "HLT", Run3 )|g' "${tmpfile}"
cat <<@EOF >> "${tmpfile}"
process.load('run362321_cff')
process.hltOnlineBeamSpotESProducer.timeThreshold = int(1e6)

# override the GlobalTag, connection string and pfnPrefix
from Configuration.AlCa.GlobalTag import GlobalTag as customiseGlobalTag
process.GlobalTag = customiseGlobalTag(
    process.GlobalTag,
    globaltag = "140X_dataRun3_HLT_v3",
    conditions = "L1Menu_CollisionsHeavyIons2023_v1_1_5_xml,L1TUtmTriggerMenuRcd,frontier://FrontierProd/CMS_CONDITIONS,,9999-12-31 23:59:59.000"
)

# run the Full L1T emulator, then repack the data into a new RAW collection, to be used by the HLT
from HLTrigger.Configuration.CustomConfigs import L1REPACK
process = L1REPACK(process, "uGT")

# to run without any HLT prescales
del process.PrescaleService

# # to run using the same HLT prescales as used online in LS 231
# process.PrescaleService.forceDefault = True
@EOF
edmConfigDump "${tmpfile}" > hlt.py

cmsRun hlt.py &> hlt.log

# remove input files to save space
rm -f run362321/run362321_ls0*_index*.*
```

## Possible extenstions

There are two more clients for which the unitTets could be activated in the future, namely:
```
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-ecalcalib_dqm_sourceclient" command="runtest.sh ecalcalib_dqm_sourceclient-live_cfg.py" /> -->
 <!-- streamDQMCalibration is required -->
 <!-- <test name="TestDQMOnlineClient-hcalcalib_dqm_sourceclient" command="runtest.sh hcalcalib_dqm_sourceclient-live_cfg.py" /> -->
```
