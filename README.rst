eoldas_examples
===============

Experiment 1 ( Savitzky-Golay smoothing)
***************************************************

The first example (in http://www2.geog.ucl.ac.uk/~plewis/eoldas/eoldas_guide.html) runs a Savitzky-Golay filter over some MODIS NDVI data. The script is ``savitzy_golay.py``, and it requires the file ``data/FuentesAndalucia_MOD09A1.txt`` that holds the data. You run the script by issuing the command ``python savitzky_golay.py``. This will pop a window, that when closed will save the plot to the images directory (this directory will be created if it doesn't exist). This plot should correspond to http://www2.geog.ucl.ac.uk/~plewis/eoldas/_images/golay.png

Experiment 2 (EOLDAS with an identity operator)
*************************************************

This experiment is described in depth in http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html. It requires two configuration files, stored in config_files: Identity.conf and eoldas_config.conf. It also requires a datafile in data/Identity/random_ndvi1.dat. The script that uses these files is solve_eoldas_identity.py. The script is executed with the command ``python solve_eoldas_identity.py``. After running this, the script will create a number of directories to store logs (mylogs/), solutions and further diagnostics (these will be under output/Identity/). The results should correspond to figures in the user's guide.

An extra script is provided in http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html#example-plotting-data-from-the-output-files. This shows how to make plots of the output using Python and Matplotlib. The required script is example1plot.py. This script will produce a plot stored under the "images" directory. It should be compared to the one on the user's manual. Similarly for solve_eoldas_identity1.py, you can use example1plot1.py to plot figures simular to those in the user's guide. Similarly, you can try solve_eoldas_identity2.py and example1plot2.py.

To plot the Hessian, as in http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html#interfacing-a-little-more-deeply-with-the-eoldas-code, you can use the script solve_eoldas_identity_a.py. It will save the plot in output/IHessianNDVI_expt1.png.

Experiment 2
**************

The second experiment requires some real MODIS observations. These are given in ``data/modis_botswana.dat``. You will also require the configuration file ``config_files/Identity2.conf``. To produce all the plots in this section, you will need to have the ``eoldas_run.py`` executable in your path (this will usually be ``~/.local/bin/``).


.. note::
 
   The command line will need to be changed from that in the user's guide to the following::

   eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/Identity2.conf --calc_posterior_unc

To run the other examples, do

eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/Identity2.conf --calc_posterior_unc --operator.modelt.rt_model.model_order=2 --parameter.x.default=5000,0.1 --operator.obs.y.result.filename=output/Identity/Botswana_fwd.params2 --parameter.result.filename=output/Identity/MODIS_botswana.params2

eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/Identity2.conf --calc_posterior_unc --operator.modelt.rt_model.model_order=2 --parameter.x.default=200,0.1 --operator.obs.y.result.filename=output/Identity/Botswana


