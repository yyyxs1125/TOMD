# TMOD
A Trail-based Off-road Multimodal Dataset for Traversable Pathway Segmentation under Challenging Illumination Conditions


## Introduction
TOMD is a multimodal dataset specifically designed to capture complex, unstructured trail-like environments using a medium-scale all-terrain robot platform. The dataset includes synchronized high-fidelity 128-channel 3D LiDAR, stereo imagery, GNSS, IMU, telemetry control signals, and ambient illumination measurements. Data was collected through repeated traversals of various routes under changing environmental conditions.

## Sensor Setup
- **LiDAR**: Ouster OS1 (128 channels), operating at 865 nm wavelength. Capable of detecting objects up to 100 m with >90% probability and 120 m with >50% probability under 100 klx sunlight and 80% Lambertian reflectivity (2048 points @ 10 Hz). Key specs include 0.3 cm range resolution, 360° horizontal FoV, and 45° vertical FoV.

- **Stereo Camera**: ZEDx dual-lens stereo camera with robust GMSL2 interface. Supports resolutions up to 2×(1920×1200) @ 60 fps and 2×(960×600) @ 120 fps, offering a maximum FoV of 110° (H) × 80° (V) × 120° (D).
  
- **IMU**: Integrated within the ZEDx camera, this IMU includes a 16-bit triaxial accelerometer and gyroscope. Provides ±12 G acceleration (0.36 mg resolution), ±1000 dps angular rate (0.03 dps resolution), with ±0.5% sensitivity error, sampled at 400 Hz.
- **GNSS**: u-blox ZED-F9P-0xB module with multi-band GNSS and RTK capabilities, embedded in the ZEDx system powered by NVIDIA Jetson Orin NX. Delivers up to 20 Hz updates with 0.01 m ± 1 ppm CEP accuracy.
  
- **Lux Meter**: Yoctopuce Light V4 ambient light sensor, with a resolution of 0.01 lux and a measurement range up to 83,000 lux at 10 Hz sampling rate.

## Data Access
You can access the full dataset via the [Durham Collection](https://collections.durham.ac.uk/collections/r2dn39x159k).
The dataset is provided in `.7z` compressed format. After downloading, please extract the archive using one of the following methods:

#### How to Uncompress `.7z` Files
- **Linux** (install `p7zip-full` if needed):
  ```bash
  sudo apt install p7zip-full
  7z x TOMD_dataset.7z
  ```
  
- **macOS**:
  Use [The Unarchiver](https://theunarchiver.com/) or install via Homebrew:
    ```bash
    brew install p7zip
    7z x TOMD_dataset.7z
    ```
    
- **Windows**:
  Use [7-Zip](https://www.7-zip.org/) GUI or right-click the `.7z` file → "Extract Here"
 
After extraction, the folder structure will look like:
```
TOMD/
  ├── TOMD_mm_dd_yy_partx/             # Sequence for a specific date and route
  │   ├── Images/                      # Stereo image frames (rectified & time-synchronized)
  │   │   ├── left/
  │   │   │   └── <timestamp>.png      # Left camera images
  │   │   └── right/
  │   │       └── <timestamp>.png      # Right camera images
  │   ├── Pointclouds/                 # LiDAR data (x, y, z, intensity)
  │   │   └── <timestamp>.npy
  │   ├── IMU/                         # Inertial Measurement Unit data
  │   │   └── imu.csv                  # timestamp, orientation (x/y/z/w), angular & linear velocity
  │   ├── GPS/                         # GNSS outputs
  │   │   ├── pvt.csv                  # timestamp, lat/lon/alt, MSL height, velocity (n/e/d)
  │   │   └── navstafix.csv            # timestamp, lat/lon/alt with RTK fix status
  │   ├── Lux/                         # Ambient light readings
  │   │   └── illuminance.csv          # timestamp, lux value
  │   └── Control/                     # Robot motion commands
  │       └── cmd_vel.csv              # timestamp, linear & angular velocities (x/y/z)
```
  
