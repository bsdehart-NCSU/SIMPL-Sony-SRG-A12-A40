# **Sony SRG-A40 / SRG-A12 VISCA IP Control SIMPL+ Module**

**Version:** 1.1

## **Overview**

This Crestron SIMPL+ module provides comprehensive and robust control for **Sony SRG-A40** and **SRG-A12** PTZ cameras over a standard TCP/IP network using the VISCA protocol.  
The module is designed for professional AV integration, offering discrete commands for nearly all camera functions and providing real-time feedback. A core feature is its seamless integration with the **Crestron C2N-CAMIDJ** joystick, enabling an intuitive and tactile control experience for camera operators.

## **Key Features**

* **Full PTZF Control:** Smooth, variable-speed pan, tilt, zoom, and focus control.  
* **Extensive CCU Settings:** Access and adjust a wide range of image parameters, including:  
  * Exposure (Auto, Manual, Shutter/Iris Priority)  
  * White Balance (Auto, Presets, One-Push, Manual)  
  * Gain, Iris, Shutter, and Aperture  
  * Image enhancements like WDR, Backlight Compensation, and High Sensitivity.  
* **Advanced Preset Management:** Store, recall, and clear up to 256 presets.  
* **C2N-CAMIDJ Joystick Integration:**  
  * Mode-based control for PTZ speed, focus, and iris.  
  * Automatic feedback to the joystick's LEDs and digital display.  
  * On-the-fly speed adjustments using the joystick wheel.  
* **Robust Communication:**  
  * Manages VISCA over IP sequence numbering and packet formatting.  
  * Automatic keep-alive polling to monitor the camera's connection status.  
  * Re-initializes the connection if communication is lost.  
* **Additional Controls:**  
  * Auto Framing activation and deactivation.  
  * Tally light control with a keep-alive mechanism.  
  * Video Mute, Image Flip, and more.

## **Compatibility**

* **Primary:** Sony SRG-A40, Sony SRG-A12  
* **Protocol:** VISCA over IP

While other Sony VISCA over IP cameras may respond to basic commands, full functionality is only guaranteed for the primary models listed.

## **Getting Started**

1. **Add to SIMPL Program:** Add a TCP/IP Client device to your SIMPL program. Set its IP Address to the static IP of the Sony camera and the port to **52381**.  
2. **Insert Module:** Drag the Sony SRG-A40 A12 VISCA IP C2N-CAMIDJ v1.1.usp module from your user modules into the Logic folder of your program.  
3. **Connect Communication:**  
   * Connect the To\_Camera\_tx$ output of the module to the TX$ input of the TCP/IP Client.  
   * Connect the RX$ output of the TCP/IP Client to the From\_Camera\_rx$ input of the module.  
4. **Control & Feedback:** Connect your control system logic (e.g., from a touch panel) to the various \_trig inputs on the module. Use the \_fb outputs to drive feedback on your user interface.  
5. **C2N-CAMIDJ (Optional):** If using a joystick, add a C2N-CAMIDJ symbol to your program and connect its analog and digital outputs to the corresponding C2N\_CAMIDJ\_ inputs on this module. Connect the module's C2N\_CAMIDJ\_ feedback outputs back to the joystick symbol.

## **Operations**

### **Initialization**

The module automatically handles the connection and initialization process. Upon a successful TCP/IP connection, it resets the VISCA sequence number and queries all camera states to synchronize feedback.

### **C2N-CAMIDJ Joystick**

The joystick provides an intuitive way to operate the camera:

* **Mode Buttons (Focus, Pan, Tilt, Zoom):** Select what the joystick and wheel will control.  
* **Speed Buttons (Fast/Slow):** Select the active speed profile for PTZ movements.  
* **Wheel:**  
  * In **Focus** or **Iris** mode, the wheel directly adjusts the setting.  
  * In a **Speed** mode, press and turn the wheel to change the speed value for the currently selected profile (Fast or Slow). The value is shown on the joystick's display.  
* **Timeout:** The joystick mode automatically reverts to its default state after 30 seconds of inactivity to prevent accidental adjustments.

### **Troubleshooting**

The Debug\_fb$ string output is the primary tool for troubleshooting. Connect it to a "Serial/ASCII Send" symbol (or view it in SIMPL Debugger) to see:

* Formatted commands being sent to the camera.  
* Parsed responses received from the camera.  
* Connection status and error messages (e.g., timeouts).

If the module fails to connect or control the camera, verify the IP Address and Port on the TCP/IP Client symbol and ensure the camera is on the network and accessible.