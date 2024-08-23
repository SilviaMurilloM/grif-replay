Grif-Replay
===============

A data sorting code for processing GRIFFIN-style [MIDAS](https://daq00.triumf.ca/MidasWiki/index.php/Main_Page) files into histograms.

## Architecture

Grif-Replay is composed of two parts; the data-sorting engine and server (written in c), and a set of browser-based web tools (javascript and html) for monitoring/controlling the data sorting and doing data analysis. This repository contains the c code which runs on a computer as a local or remote server. The browser code is in the [SpectrumViewer](https://github.com/GRIFFINCollaboration/SpectrumViewer) repository of the GRIFFINCollaboration GitHub.

## Installation

Download the repository from GitHub into your chosen working directory. Then in the working directory just run `make`.

## Running Grif-Replay

### Launch the server

Once the code has been successfully compiled you can run it. If you will be running this as a remote server then it is a good idea to run Grif-Replay inside a screen session or similar.

Navigate to the working directory where Grif-Replay was compiled. You can launch Grif-Replay with the command:

`./grif-replay`

The output on the terminal does not need to be monitored (you can detach from the screen session now). From this point you will interact with Grif-Replay through the interface in your web browser.

### Connect the web interface

Open a web browser and navigate to the following URL:
`https://griffincollaboration.github.io/SpectrumViewer/analyzerInterface.html?backend=localhost&port=9093`

If you are connecting to a remote instance of Grif-Replay running on another computer than replace the `backend=localhost` part of this URL with the name of the computer hosting the server. For example if you want to connect to an instance of Grif-Replay running of the computer grifstore0 then the URL would be:
`https://griffincollaboration.github.io/SpectrumViewer/analyzerInterface.html?backend=grifstore0&port=9093`

### Set the paths

Set the paths to the directories of the computer running the GRIF-Replay server using the text boxes of the `Sort MIDAS files`:
MIDAS Data File Directory = the directory containing the .mid files to be sorted.
Histogram File Directory = the directory where the .tar histogram output files will be written (can be the same as MIDAS Data File Directory).
Configuration File Directory = the directory to store the configuration file with Grif-Replay settings.

### Sort MIDAS files

Ensure you are on the `Sorting Control` subpage of the Web Interface. In the table at the bottom, click on the title of the MIDAS file to be sorted so that the row will be highlighted. Click the `Submit selected files to the sorting queue`. The sorting progress can be monitored in the box at the top right of the Web Interface.

### Connect to Online

Click on the button `Connect to online MIDAS` for the appropriate server name.

### View histograms

There are a couple of ways to open the .tar histogram files to view spectra. The methods all launch the spectrum viewer with appropriate URL arguments to open directly the file. One can also open the spectrum viewer and open a file by selecting the directory and histogram file name.

On the `Sorting Control` subpage of the Web Interface click on the `Open Histo file` link in the table next to the run.

On the `Spectrum Viewer & Analysis` subpage of the Web Interface click on the title of the histogram file in the table, or click on the `Open in 2D Viewer` link in the same row.

### Convert histogram .tar files to Root format

In a terminal, navigate to the working directory, or any directory containing the tar2root.C script.
Open `grsisort` or `Root`.
run the command

`.x tar2root.C("/tig/grifstore1/grifalt/schedule146/S2232/runXXXX.tar","runXXXX.root)`

The runXXXX.root histogram file can now be opened and viewed in Root or GRSISort.

## Development

Grif-Replay was originally developed by Chris Pearson (data-sorting engine and server) and Adam Garnsworthy (browser tools) at TRIUMF Inc. during the 2023-2024 time period. The browser tools use much of the infrastructure originally developed by Bill Mills during the 2013-2016 time period.
