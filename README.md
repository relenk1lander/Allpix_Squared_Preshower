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
- The import of the real data from the ASIC is done from `data.csv`. THe first line contains the injected charge in each pixel. After the second line each line is the resulting ADC values from one pixel. In some cases very low injections of charge do not give ADC values in some of the pixels.
- The result in the root files from the  `CalibrationFlatTreeWriter` and `CalibrationTreeWriter` are the true charge, the ADC value for that charge and the reconstructed (calibrated) charge.

### Neutrino Events:
- The import of the GENIE files is done in  **`DepositionGenerator`**.
- The neutrino events are genrated randomly around the tungsten area of the preshower detector. 

### Analysis:
- For analysis, use the **`CalibrationFlatTreeWriter`** module (preferred by the team) or the alternative **`CalibrationTreeWriter`**.
- The file `asic_map.cpp` makes the heatmap of one of the central ASICs of the preshower detector. In my case the ASIC that I shot the photons. You can adapt this depending on the ASIC map you want to plot. You can also adjust it based on whether you want to plot the zoomed ASIC or the full ASIC. This cpp file is for the output root file from the `CalibrationTreeWriter`.
- Example root files from 2 photons shot with 1 TeV energy each and distance 200 microns can be found here: [here](https://drive.google.com/drive/folders/1u6vDf8uHQeF3-Sme_m_0nZH-jpewMtyE?usp=sharing)

### Geometry:
- The detector geometry is defined in the `geometry_preshower.conf` file.
- In the geometry configuration file the ASICs are depicted with: `[Detector_0_#_#]`. The first number represents the number of plane, starting from 0. For six planes: 0,1,2,3,4,5,6. Therefore if you wish to simulate some planes without ASICs, just delete the corresponding ASICs. For intsance if you do not want to have the ASICs from plane 3, you can delete all the detectors with: `[Detector_2_#_#]`.

---
