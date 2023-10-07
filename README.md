
# Stream Locations FUSE Filesystem

Stream Locations FUSE Filesystem (Filesystem in Userspace) maps files from it source location, creating the corresponding STRM in the destination location on-the-fly.

## Table of Contents

-  [Requirements](#requirements)
-  [Installation](#installation)
-  [Usage](#usage)
	-  [Mounting with fstab](#mounting-with-fstab)
-  [Configuration](#configuration)
-  [Troubleshooting](#troubleshooting)
-  [Roadmap](#roadmap)
-  [Contributing](#contributing)
-  [License](#license)

## Requirements

To use this project, you'll need the following prerequisites:

- Python 3.x
-  [fusepy](https://github.com/fusepy/fusepy) library
-  [PyYAML](https://pyyaml.org/) library (for configuration file support)

You can install the required libraries using `pip`:
```bash
$ pip  install -r requirements.txt
```

## Installation

1. Clone or download this repository to your local machine.
2. Install the required Python libraries (fusepy and PyYAML) using the command mentioned in the "Requirements" section.

## Usage

To use the Stream Locations FUSE Filesystem, follow these steps:

1. Open a terminal and navigate to the project directory.
2. Run the FUSE filesystem by executing the script.
	```bash
	$ ./strmfs  source_directory  destination_directory  -o  mount_options
	```
	Replace source_directory with the path to your media files, destination_directory with the path where you want to mount the filesystem, and mount_options with any optional FUSE mount options you want to specify.

3. Access and stream your video files in .strm format from the mounted filesystem.

## Mounting with fstab

To make the Stream Locations FUSE Filesystem mount at boot time or by a specific user, you can use the /etc/fstab file on Linux. Here's how to add an entry to mount it:

1. Open a terminal.
2. Edit the /etc/fstab file using a text editor with root privileges (e.g., sudo nano /etc/fstab).
3. Add the following line to the /etc/fstab file, replacing the placeholders with your specific paths and options:

```vim
/path/to/source_dir  /path/to/destination_dir  fuse.strmfs  mount_options  0  0
```

* Replace /path/to/source_diry with the path to your source directory.
* Replace /path/to/destination_dir with the path where you want to mount the filesystem.
* Replace mount_options with any FUSE mount options you want to specify.

4. Save and close the /etc/fstab file.

To test the new entry without rebooting, run the following command:

```bash
sudo  mount  -a
```

This will attempt to mount all entries in /etc/fstab.

Now, the Stream Locations FUSE Filesystem will be mounted automatically at boot time or when the mount -a command is executed.

## Configuration

The project supports a configuration file in YAML format (config.yaml) for setting default mount options. You can place this file in the following locations:

* System-wide configuration: /etc/strmfs/config.yaml
* User-specific configuration: ~/.config/strmfs/config.yaml

The configuration file should have the following format:

```yaml
mount_options:
    allow_other:  true
    foreground:  false
    nothreads:  true
    file_types:  "mp4+mkv+mov+m4v+mpg+mpeg+avi+flv+webm+wmv"
```

You can customize the default mount options in this configuration file.

## Troubleshooting

If you encounter any issues while using the Stream Locations FUSE Filesystem, here are some common troubleshooting steps:

### FUSE Filesystem Is Not Mounting

Ensure that you have the required permissions to mount FUSE filesystems. You may need to run the script with administrative privileges (e.g., sudo python strmfs).

### Video Playback Problems

Check the source directory for valid video files in supported formats (e.g., .mp4, .mkv). Ensure that the file extensions are correctly set to .strm for streaming.

### Configuration Not Applied

Verify that your configuration file (config.yaml) is in the correct location (either /etc/strmfs/ for system-wide or ~/.config/strmfs/ for user-specific). Ensure that the YAML syntax is correct.

### Python Library Dependencies

Double-check that you have installed the required Python libraries (fusepy and PyYAML) using pip. Update them if necessary.

**If your issue persists or you encounter a different problem, please open an issue on our GitHub repository with detailed information about the problem you're experiencing.**