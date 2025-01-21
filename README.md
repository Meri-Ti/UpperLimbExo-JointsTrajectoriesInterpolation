# UpperLimbExo-JointsTrajectoriesInterpolation

This repository contains MATLAB scripts used to analyze and plot the joint trajectories during horizontal abduction (H. Abd) movements at 30°, 60°, and 120° for a upper limb exoskeleton. Each script processes a specific set of recorded logs and generates relevant plots for trajectory visualization with the Gaussian resistive control strategy.

## Files in the Repository

1. **`ex_trsp_habd30.xcs`** – Data log for horizontal abduction at 30°.
2. **`ex_trsp_habd60.xcs`** – Data log for horizontal abduction at 60°.
3. **`ex_trsp_habd120.xcs`** – Data log for horizontal abduction at 120°.

## Code Overview

The primary MATLAB script (`plot_trajectories.m`) performs the following tasks:

- **Data Loading**: Reads the log files and extracts joint angles for each joint involved in the horizontal abduction.
- **Trajectory Calculation**: Identifies the start and end times of each movement and shifts the time axis to start from 0.
- **Plotting**: Generates individual trajectory plots for each joint, highlighting the time when the middle position is reached with a dashed line. It also saves the generated plots as SVG files.
- **Linear Interpolation**: For Joint 6, the code computes a linear interpolation for the recorded movement. This interpolation is plotted and compared to the original trajectory.
- **Polynomial Fitting**: The code fits a 5th-degree polynomial for each joint angle relative to Joint 6's trajectory, allowing smooth interpolation of joint movements.

## Plots

The script generates several plots:

1. **Individual Joint Trajectories**: For each joint (J1-J7), the original trajectory is plotted over time, with a vertical line marking the midpoint of the movement.
2. **Linear Interpolation of Joint 6**: A plot comparing the original recorded trajectory of Joint 6 with the linear interpolation over time.
3. **Polynomial Fitting for Each Joint**: For each joint, the trajectory is fitted with a 5th-degree polynomial relative to the movement of Joint 6.

## Usage

1. Clone this repository:
    ```bash
    git clone https://github.com/Meri-Ti/UpperLimbExo-JointsTrajectoriesInterpolation.git
    ```
2. Open MATLAB and run the script `plot_trajectories.m` for each angle (30°, 60°, or 120°):
    ```matlab
    run('plot_trajectories.m')
    ```
3. The generated plots will be saved as SVG files in the working directory.

## Example Plots

Below are examples of the generated trajectory plots:

- **Joint 6 Linear Interpolation (H. Abd 30°)**:
    ![J6 Linear Interpolation](path_to_image/J6_interp30.svg)

- **Joint 1 Polynomial Fitting (H. Abd 30°)**:
    ![J1 Polynomial Fitting](path_to_image/J1_5thInterp30.svg)



# Plot Rigid Body Tree with Joint Trajectory from Log File

1. **`ResistiveEMG_30.mlx`** – Live script for horizontal abduction at 30°.
2. **`ResistiveEMG_60.mlx`** – Live script for horizontal abduction at 60°.
3. **`ResistiveEMG_90.mlx`** – Live script for horizontal abduction at 90°.

This repository provides MATLAB code, first to visualize the trajectory of Joint 6 (J6) of the FloatEVO exoskeleton from a log file, since it was the joint which guides the overall exercise during H. Abd. 30°, 60°, and 90°. The code also allows for the extraction and plotting of specific time intervals for different Gaussian resistance levels (low, medium, high) over 30°, 60°, and 90° elevation angles for the H.Abd.
Then the Gaussian profile for the resistive torque is plotted considering the three different levels of resistance (low, medium, and high).
The following description referes only to the **`ResistiveEMG_30.mlx`** MATLAB code.

## Features

- **Log File Import**: Reads trajectory data for J6 from a log file.
- **Time Adjustment**: Shifts time to start from `t = 0`.
- **Highlight Time Intervals**: Highlights specific resistance levels in the J6 trajectory.
- **Customizable Visualization**:
  - Font sizes, colors, and legend styles can be adjusted.
  - Allows extraction of trajectories within specific time intervals.
- **Save Plots**: Saves the generated plots as SVG files.

## Prerequisites

- MATLAB installed on your system.
- The log file for J6 from the FloatEVO exo (`Joint6.log`).

## File Description

- `Joint6.log`: The input log file containing time and trajectory data for J6.

## Instructions

1. **Set Up Log File**: Place your log file in the same directory as the script or update the `filename` variable in the script to the correct file path.

   ```matlab
   filename = 'Joint6.log';  % Update this with the correct file path
   ```

2. **Run the Script**: Execute the MATLAB Live script to generate plots.

3. **Time Intervals**: The resulting plots show the different resistance levels

   - **High Resistance**
   - **Medium Resistance**
   - **Low Resistance**

    highlighting the start and the end of each one.
  
4. **Output Plots**:
   - `J6Traj_S1_GaussRes.svg`: Plot showing the full J6 trajectory with highlighted H. Abd. executed.
   - `J6Traj_S1_HABD30.svg`: Plot focused on the 30° Gaussian resistance interval with labels highlighting the start and the end for each one of the three resistance levels.

## Customization

You can modify the following parameters to suit your visualization needs:

- **Font Sizes**:

  ```matlab
  label_fontsize = 38;
  title_fontsize = 42;
  tick_fontsize = 34;
  legend_fontsize = 34;
  ```

- **Figure Dimensions**:

  ```matlab
  figure_size = [100, 100, 1600, 1300];
  ```

- **Colors**: Customize the colors for different intervals by modifying `PS.Red1`, `PS.DYellow1`, etc.

# Gaussian Resistance Torque Simulation

Then, the code simulates a robotic system with Gaussian resistive torque applied to specific joint positions.
The implementation includes data processing, visualization, and trajectory tracking. Below teh details.

---

## Code Structure and Workflow

### 1. Load and Process Joint Data

- **File**: `Joint*.log` extracted from the FloatEVO exo for the overall 7 joints.
- The program reads joint data for 7 joints from log files.
- It computes time shifts and defines time intervals for different resistance levels (low, medium, high).

### 2. Gaussian Resistive Torque (Low Resistance)

- **Formula**:
- Parameters:
  - **Max Torque**: `5 Nm`, the maximum available of the Gaussian profile
  - **Desired Max Torque**: `0.5 * Max Torque`, the actual maximum reached
  - **Sigma (****)**: `0.5 rad`, the standard deviation
  - **Mean Shift (****)**: `1.457 rad`, the point where to centre the Gaussian peak
- Plots the Gaussian torque profile with color gradients representing resistive torque with different intensity.

### 3. Rigid Body Tree Visualization

- Uses MATLAB's `show()` function to render the robot.
- Labels all joints and the end-effector (EE).
- Visualizes joint trajectories with gradient coloring based on resistive torque values.

### 4. Key Functions

#### `timeToIndex(timeData, targetTime)`

- Converts a time value into the corresponding index in the time data.

#### `extractAngles(jointAngles, startIdx, endIdx)`

- Extracts joint angles for a specific time interval.

---

## Outputs

1. **Gaussian Torque Profile**

   - File Names:
     - `LowGaussProfileHabd30.fig`
   - Visualizes the Gaussian torque for low Gaussian resistance with peak torque and sigma indicators.

2. **Trajectory Visualization**

   - File Names:
     - `LowGaussResTraj_S1.svg`
   - 3D trajectory of the end-effector visualized with a rigid body tree and color-coded segments.

---

## How to Run

1. Clone the repository and ensure all log files (`Joint1.log` to `Joint7.log`) are in the same directory.
2. Open MATLAB and set the current folder to the project directory.
3. Run the main script to process the data and generate figures.
4. Outputs will be saved in the project directory.

---

## Repository Files

- `ResistiveEMG_30.mlx`: Main MATLAB script.
- `Joint*.log`: Log files containing joint data.
- Output files: Saved `.fig`, and `.svg` visualizations.

---
