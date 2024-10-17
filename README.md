# UpperLimbExo-JointsTrajectoriesInterpolation

This repository contains MATLAB scripts used to analyze and plot the joint trajectories during horizontal abduction (H. Abd) movements at 30°, 60°, and 120° for a upper limb exoskeleton. Each script processes a specific set of recorded logs and generates relevant plots for trajectory visualization.

## Files in the Repository

1. **`ex_trsp_habd30.xcs`** – Data log for horizontal abduction at 30°.
2. **`ex_trsp_habd60.xcs`** – Data log for horizontal abduction at 60°.
3. **`ex_trsp_habd120.xcs`** – Data log for horizontal abduction at 120°.
4. **`plot_trajectories.m`** – MATLAB script for processing and plotting joint trajectories at different angles.

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
