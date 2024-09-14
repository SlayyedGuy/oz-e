# OZ Shell Script

## About

OZ Shell Script provides dynamic temperature-based control over CPU frequencies and fan speeds on Linux systems.
By regulating CPU performance to maintain optimal temperatures, it ensures system stability and longevity.

## Requirements

- A Linux-based system
- CPU temperature monitoring capabilities
- Optional: The OZ Fan Controller Module for fan speed control

## Configuration

1. Clone the OZ repository to your local machine.
2. Create a new configuration file (you can use `OZ.config.sample` as a template) with a text editor.
3. Configure the configuration file variables to match your system setup and preferences.
4. Save changes.

## Configuration with Hardware Module

If you have the OZ Fan Controller Module installed:
1. Follow the hardware setup instructions provided with the module.
2. Ensure that the serial device path (`fanSerialDevice`) in the configuration file points to the correct device.
3. Specify the number of fans (`noOfFans`) connected to the module.
4. Adjust the fan speed curves in the configuration file to match your cooling requirements.

## Starting + Command Line Options

To start OZ:
1. Open a terminal window.
2. Navigate to the directory containing the script (`OZ.sh`).
3. Run the script using the following command:

```bash
./OZ.sh -t SECONDS_TO_RUN -c CONFIG_FILE
```

Command Line Options:
- `-t SECONDS_TO_RUN`: Specify the duration (in seconds) for which OZ will run.
- `-c CONFIG_FILE`: Specify the path to the configuration file.
- `-h`: Displays help.

Example usage:
```bash
./OZ.sh -t 62 -c config.txt
```

This command starts OZ, running for 62 seconds, using the configuration specified in `config.txt`.


## Cron Job Entry

To run OZ automatically at regular intervals, you can use a cron job. Here's an example crontab entry:
```
* * * * * /bin/sh /usr/local/bin/OZ.sh -t 62 -c /usr/local/etc/OZ.config > /dev/null
```
This will run the script every minute and execute it for 62 seconds (as specified with the `-t` parameter). Verify that you have
correctly entered the paths for `OZ.sh` and `OZ.config` files.


## Safety Considerations

**!!! WARNING: You are using this software at your own risk. Improperly configured or wired fan controller modules can damage your
hardware. Setting fan speeds too low can lead to overheating, which can also cause damage to your hardware. !!!**

To ensure safe operation:

- Ensure that the fan controller module is correctly connected and configured to avoid damaging hardware due to inadequate cooling.
- Use CAUTION when defining fan speed curves and temperature thresholds to prevent overheating and oscillations.
- Follow the safety principles or there will be problems!

## Contributions

Contributions to OZ are welcome!
Whether you're a seasoned developer or a newcomer, we appreciate all contributions that help improve OZ for the community.

## Support

For any questions, issues, or feedback, please open an issue on GitHub.

---
Copyright (c) 2024 ARSARK Developers
