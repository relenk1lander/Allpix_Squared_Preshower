# Allpix Squared - Final Detector Effects for FASER

This repository contains all the necessary files and configurations for simulating detector effects in the FASER preshower detector using the Allpix Squared framework.

**Repository Link:** [Allpix Squared Final Detector Effects for FASER](https://gitlab.cern.ch/rkotitsa/allpix-squared/-/tree/final_detector_effects_faser?ref_type=heads)


---

## Repository Overview

### Folder Structure:
1. **`workspace`**: For simulations with photons, muons, and other particles (excluding neutrinos).
2. **`workspace_genie`**: For simulations with neutrinos.

---

## Running Simulations

### **Simulations with Photons, Muons, etc. (Non-Neutrinos)**
1. Navigate to the `workspace` folder:
   ```bash
   cd workspace
   ```
2. Run the simulation:
   ```bash
   ../bin/allpix -c run.conf
   ```

#### Required Files in `workspace`:
- **`run.conf`**: The main configuration file.
- **`data.csv`**: Real data from the ASIC for digitization and calibration.
- **`geometry_preshower.conf`**: Configuration for the preshower detector.
- **`gps.mac`**: Defines particle energy and other simulation parameters.

---

### **Simulations with Neutrinos**
1. Navigate to the `workspace_genie` folder:
   ```bash
   cd workspace_genie
   ```
2. Run the simulation:
   ```bash
   ../bin/allpix -c run_genie.conf
   ```

#### Required Files in `workspace_genie`:
- **`run_genie.conf`**: Updated main configuration file with the `DepositionGenerator`.
- **`geometry_preshower.conf`**: Configuration for the preshower detector.
- **`data.csv`**: Real data from the ASIC for digitization and calibration.
- **Root File**: Required root file from GENIE software. The GENIE neutrino samples from the FASERnu team can be found here: `/eos/project/f/faser-preshower/neutrino-simulation-input`
-  Add the desired file (`nu_mu`, `nu_e`, or `nu_tau`) to the `workspace_genie` folder. The simulation runs with the file with this name: `nue_faser_1M.dump.root`, `nutau_faser_1M.dump.root`, `numu_faser_1M.dump.root`

---

## Additional Notes

### Configuration Files:
- **ASIC Configuration**: Located in the `models` folder as `faser.conf`.

### Calibration:
- Calibration is done using the **`Calibration`** module.
- For analysis, use the **`CalibrationFlatTreeWriter`** module (preferred by the team) or the alternative **`CalibrationTreeWriter`**.

### Geometry:
- No GDML file is used for the geometry.
- The detector geometry is defined in the `geometry_preshower.conf` file.

### TCAD Simulations:
- TCAD simulations were conducted by Jordi.
- The electric field map may not be fully finalized due to the large size of the FASER ASIC. Further details will be confirmed during the meeting.

---

For any questions or further assistance, feel free to reach out during the remaining time of my contract.
