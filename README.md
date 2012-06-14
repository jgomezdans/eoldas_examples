eoldas_examples
===============

Experiment 1 ( Savitzky-Golay smoothing)
***************************************************

The first example (in http://www2.geog.ucl.ac.uk/~plewis/eoldas/eoldas_guide.html) runs a Savitzky-Golay filter over some MODIS NDVI data. The script is ``savitzy_golay.py``, and it requires the file ``data/FuentesAndalucia_MOD09A1.txt`` that holds the data. You run the script by issuing the command ``python savitzky_golay.py``. This will pop a window, that when closed will save the plot to the images directory (this directory will be created if it doesn't exist). This plot should correspond to http://www2.geog.ucl.ac.uk/~plewis/eoldas/_images/golay.png

Experiment 2 (EOLDAS with an identity operator)
*************************************************

This experiment is described in depth in http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html. It requires two configuration files, stored in config_files: Identity.conf and eoldas_config.conf. It also requires a datafile in data/Identity/random_ndvi1.dat. The script that uses these files is solve_eoldas_identity.py. The script is executed with the command ``python solve_eoldas_identity.py``. After running this, the script will create a number of directories to store logs (mylogs/), solutions and further diagnostics (these will be under output/Identity/). The results should correspond to figures in the user's guide.

An extra script is provided in http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html#example-plotting-data-from-the-output-files. This shows how to make plots of the output using Python and Matplotlib. The required script is example1plot.py. This script will produce a plot stored under the "images" directory. It should be compared to the one on the user's manual. Similarly for solve_eoldas_identity1.py, you can use example1plot1.py to plot figures simular to those in the user's guide. Similarly, you can try solve_eoldas_identity2.py and example1plot2.py.




