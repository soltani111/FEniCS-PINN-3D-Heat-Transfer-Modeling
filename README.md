# Laser-Induced Fluorescence (LIF) Method for Temperature Measurement

## Test Theory

The one-color LIF method was used to calculate the temperature in this experiment. The fluorescent property of the particles was utilized by shining laser light on them, stimulating the particles, and measuring the intensity of the emitted light to determine the temperature of the fluid.

Fluorescent materials emit light when exposed to laser light at a specific wavelength. This emitted radiation is temperature-dependent and ceases immediately when the external light source is removed. The degree of temperature dependence varies across different fluorescent materials, with most materials showing increased radiation intensity as the temperature decreases.

### Quantum Efficiency

The quantum efficiency \( Q \) can be defined as:

\[
Q = \frac{\text{Emitted Intensity}}{\text{Incident Intensity}}
\]

In this relationship, several factors such as \( K_{\text{spec}} \), \( K_{\text{opt}} \), \( \epsilon_1 \), \( \epsilon_2 \), \( C \), \( I_0 \), \( b \), and \( z \) represent various coefficients and parameters influencing the intensity of the fluorescent radiation, absorption by the material, and the laser light path.

### Considerations in the Experiment

In the experiment, the concentration of fluorescent particles is uniform throughout the container. Assuming low laser light fluctuations and low concentration, the term \( e^{-c(\epsilon_1 b + \epsilon_2 z)} \) can be approximated as 1.

To calculate the temperature from the light intensity, the ratio of the radiation intensity in the test mode to that in the reference mode is used:

\[
\frac{I_f}{I_{f_{\text{ref}}}} = e^{\beta \left(\frac{1}{T} - \frac{1}{T_0}\right)}
\]

To determine the temperature distribution, the coefficient \( \beta \) is needed, which is obtained using a calibration curve from a separate experiment.

### Test Equipment

The test setup includes a laser and a cylindrical lens to create a light sheet in the test container. A camera is placed perpendicular to the laser sheet, focused on the area of interest. Rhodamine B is used as the fluorescent substance, which is dissolved in water to create a solution of specific concentration. A filter is applied to the camera to block the laser light and only allow the emitted fluorescent light to pass through.

### Description of the Experiment

1. **Concentration Measurement**: Dissolve Rhodamine B in water and ensure uniform distribution using a magnetic stirrer. The concentration of this solution is measured as a reference.

2. **Injection and Measurement**: Inject a concentrated fluorescent solution into a dilute solution using a syringe, taking images to measure concentration over time.

3. **Temperature Measurement**: Stir the solution uniformly, measure its initial temperature (26°C), and take reference images. Heat the solution to 53°C while stirring and take images at this elevated temperature to create a calibration curve. Inject cold fluid into the container and take images to determine the temperature distribution using the calibration curve.

## Conclusion

Using the LIF method, the temperature distribution within a fluid can be determined accurately by analyzing the emitted light from fluorescent particles. This method is effective for non-intrusive temperature measurements in various experimental setups.
