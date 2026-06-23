# Zero-Config Plug-and-Play Art-Net HUB75(E) Controller

This project implements a zero-configuration, plug-and-play Art-Net controller on the **Colorlight 5A-75E v8.2** board (Lattice ECP5 LFE5U-25F). It dynamically detects and configures scan timing and layout mapping on the fly by analyzing the incoming Art-Net universe streams.

## Features
	
	*   **12 Concurrent Ports**: Drives up to 12 active HUB75(E) output ports (J1 - J12) simultaneously.
	*   **Dynamic Auto-Detection**: Each port automatically configures its scan rate and shift layout based on active universe patterns.
	*   **Mixed Sizes Supported**: Supports 64x64, stacked 32x64 pairs (behaving as a single logical 64x64 panel), standard 32x64, and standard 32x32 panels.
	*   **5-Bit Color Depth**: Memory-optimized BRAM implementation providing 32,768 colors.
	*   **Flicker-Free Watchdog**: Auto-blanks all panels within 0.5s if the Art-Net stream is interrupted.

---
## Default IP Address

	10.10.10.10 

## Changing the IP Address
     
	Set UNIVERSE 969 to a Static Address with channels 1-4. ie: uni969:(ch1.ch2.ch3.ch4)
	Set UNIVERSE 969 to 000.000.101.010 to accept a DHCP address.
	 (This is 42 in binary. It is the answer to life, the universe, and everything.) 

## Art-Net Universe Layout Mapping (33 Universes Per Port)

	JJ1 - UNIVERSE 0-35
	J2 - UNIVERSE 36-71
	J3 - UNIVERSE 72-107
	J4 - UNIVERSE 108-143
	J5 - UNIVERSE 144-179
	J6 - UNIVERSE 180-215
	J7 - UNIVERSE 216-251
	J8 - UNIVERSE 252-287
	J9 - UNIVERSE 288-323
	J10 - UNIVERSE 324-359
	J11 - UNIVERSE 360-395
	J12 - UNIVERSE 396-431


## How to use the automatic configuration:

	For a 64x64 panel (2 rows per universe) (1/32 scan): Set your output to map universes 0–31 (leave 32–35 empty).
	For 2 32x64 panels daisy-chained together (2 rows/universe) (1/16 scan): Set your output to map universes 0–15 and 17–32 (leave 16 and 33–35 empty).	
	For a single 32x64 panel (2 rows/universe) (1/16 scan): Set your output to map universes 0–15 (leave 16–35 empty).
	For a single 32x32 panel (4 rows/universe) (1/16 scan): Set your output to map universes 0–7 (leave 8–35 empty).
	For 2 32x32 panels daisy-chained together (4 rows/universe) (1/16 scan): Set your output to map universes 0–7 and 9–16 (leave 8 and 17–35 empty).	
	For 3 32x32 panels daisy-chained together (4 rows/universe) (1/16 scan): Set your output to map universes 0–7, 9–16, and 18–25 (leave 8, 17, and 26–35 empty).
	For 4 32x32 panels daisy-chained together (4 rows/universe) (1/16 scan): Set your output to map universes 0–7, 9–16, 18–25, and 27–34 (leave 8, 17, 26, and 35 empty).
---

## Physical Reset Button (Revert to 10.10.10.10)
	
	Press & Hold: Press and hold the onboard user button (button SITE R7).
	Visual Blinking Feedback: As soon as the button is pressed, the status LED will override its normal heartbeat and start blinking rapidly (~7.5 Hz) to show that the 10-second timer is counting down.
	Reset Triggered: Keep holding the button for 10 seconds. Once the 10-second threshold is met, the status LED will turn solid ON.
	IP Restored: The board's IP address instantly reverts back to 10.10.10.10.
	Release Button: Once you release the button, the LED reverts to its normal heartbeat blink.


## Sources & References

	This implementation relies on the following resources:
		*   **Ethernet MAC/PHY Core**: Generated using [LiteEth](https://github.com/enjoy-digital/liteeth) by Florent Kermarrec / Enjoy-Digital.
		*   **Toolchain**: Compiled using the open-source FPGA toolchain [Yosys](https://github.com/YosysHQ/yosys) (synthesis) and [nextpnr-ecp5](https://github.com/YosysHQ/nextpnr) (place-and-route).
		*   **Flashing Utility**: Programmed over JTAG using [openFPGALoader](https://github.com/trabucayrog/openFPGALoader).
		*   **AI Pair Programmer**: Co-designed, implemented, and optimized by **Antigravity** (Google DeepMind's AI coding assistant).
			Thank You All!