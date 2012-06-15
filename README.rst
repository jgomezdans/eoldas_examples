====================
EOLDAS examples
====================

.. contents:: :local:
    
    
Installation
=============

This repository holds the code and ancillary files that are required to run the
examples in the `EOLDAS user's guide <http://www2.geog.ucl.ac.uk/~plewis/eoldas/index.html>`_. 

However, we first need to install EOLDAS and any other modules that are required
(in this case, RT codes that are distributed as independent packages).

Installing the RT codes
************************

.. note::
    
    The semidiscrete python package is a requirement for eoldas, but it would appear that my version of 1/2discrete is somehow broken. In order to get this to work, you need the ``*.so`` object to be the one from Lewis' directory, ``/data/geospatial_10/plewis/src2/python/eoldas/doc/eoldaslib/rtmodel_ad_trans1.so``. I will have to look at how this can be fixed, but in the mean time, you need to install the semidiscrete packageS as follows ::
        
        $ cp -r /home/ucfajlg/Data/python/semidiscrete_plethora <somewhere>
        $ cd <somewhere>
        $ for i in {1..4}; do cd semidiscrete$i; python setup.py install --user ; cd ..;done
        $ cd ~/.local/lib/python2.7/site-packages/
        $ for i in {1..4}; do cp /data/geospatial_10/plewis/src2/python/eoldas/doc/eoldaslib/rtmodel_ad_trans$((i-1)).so semidiscrete$i/ ; done
        $ for i in {1..4}; do echo "from rtmodel_ad_trans$((i-1)) import *"| cat - semidiscrete$i/__init__.py > /tmp/out && mv /tmp/out semidiscrete$i/__init__.py;done
        

Installing eoldas
*********************
Simply, download the relevant code from `github.com <https://github.com/jgomezdans/eoldas/zipball/master>`_, unpack it, and then run the command ::
    
    python setup.py install --user
    
This will install things in ``~/.local/lib`` and ``~/.local/bin``. The latter might be added to your ``$PATH`` to gain access to ``eoldas_run.py``.
    


Experiment 1 ( Savitzky-Golay smoothing)
==============================================

The first example (in  `here <http://www2.geog.ucl.ac.uk/~plewis/eoldas/eoldas_guide.html>'_) runs a Savitzky-Golay filter over some MODIS NDVI data. The script is ``savitzy_golay.py``, and it requires the file ``data/FuentesAndalucia_MOD09A1.txt`` that holds the data. You run the script by issuing the command ``python savitzky_golay.py``. This will pop a window, that when closed will save the plot to the images directory (this directory will be created if it doesn't exist). This plot should correspond to `this one <http://www2.geog.ucl.ac.uk/~plewis/eoldas/_images/golay.png>`_

Experiment 2 (EOLDAS with an identity operator)
====================================================

This experiment is described in depth in `here <http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html>`_. It requires two configuration files, stored in config_files: ``Identity.conf`` and ``eoldas_config.conf``. It also requires a datafile in ``data/Identity/random_ndvi1.dat``. The script that uses these files is ``solve_eoldas_identity.py``. The script is executed with the command ``python solve_eoldas_identity.py``. After running this, the script will create a number of directories to store logs (``mylogs/``), solutions and further diagnostics (these will be under ``output/Identity/``). The results should correspond to figures in the user's guide.

An extra script is provided in `here <http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html#example-plotting-data-from-the-output-files>`_. This shows how to make plots of the output using Python and Matplotlib. The required script is ``example1plot.py``. This script will produce a plot stored under the ``images`` directory. It should be compared to the one on the user's manual. Similarly for ``solve_eoldas_identity1.py``, you can use ``example1plot1.py`` to plot figures simular to those in the user's guide. Similarly, you can try ``solve_eoldas_identity2.py`` and ``example1plot2.py``.

To plot the Hessian, as in `here <http://www2.geog.ucl.ac.uk/~plewis/eoldas/example1.html#interfacing-a-little-more-deeply-with-the-eoldas-code>`_, you can use the script ``solve_eoldas_identity_a.py``. It will save the plot in ``output/IHessianNDVI_expt1.png``.

Experiment 2 (smoothing of MODIS observations)
=====================================================

The second experiment requires some real MODIS observations. These are given in ``data/modis_botswana.dat``. You will also require the configuration file ``config_files/Identity2.conf``. To produce all the plots in this section, you will need to have the ``eoldas_run.py`` executable in your path (this will usually be ``~/.local/bin/``).


.. note::
 
   The command line will need to be changed from that in the user's guide to the following (assuming you have  ``~/.local/bin/`` in your ``$PATH``) ::

eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/Identity2.conf --calc_posterior_unc

To run the other examples, do ::

eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/Identity2.conf --calc_posterior_unc --operator.modelt.rt_model.model_order=2 --parameter.x.default=5000,0.1 --operator.obs.y.result.filename=output/Identity/Botswana_fwd.params2 --parameter.result.filename=output/Identity/MODIS_botswana.params2

eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/Identity2.conf --calc_posterior_unc --operator.modelt.rt_model.model_order=2 --parameter.x.default=200,0.1 --operator.obs.y.result.filename=output/Identity/Botswana

Experiment 3 (RT observation operators )
================================================

Radiative transfer modelling for optical remote sensing. In this experiment, we will use the semidiscrete model to invert and forward model real observations from spaceborne sensors. The first experiment gets a single observation from MERIS (15 bands in the visible/near-infrared range), and inverts this observation. The command to run it is: ::

~/.local/bin/eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/meris_single.conf --parameter.limits='[[232,232,1]]' --calc_posterior_unc

The solution will appear in ``output/meris/``, where you can find both the text files and plots that are in the users' guide.

A second example uses the results from the first, and uses the estimated state of the land surface to provide a prediction of the reflectance that would be seen by the MODIS sensor on that same day. This is then compared to the actual observations. The command is ::

~/.local/bin/eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/meris_single.conf --parameter.limits='[[232,232,1]]' --passer --conf=config_files/modis_single.conf 

Other experiments in that section are: ::

~/.local/bin/eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/meris_single.conf --parameter.limits='[[232,232,1]]' --passer --conf=config_files/modis_single_a.conf 

(the output for this will be in e.g. ``output/modis/MODIS_WW_1_A_1.fwd_a.plot.y.png``). The following experiment will be ::
    
eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/meris_single.conf --parameter.limits='[[232,232,1]]' --conf=config_files/modis_single_b.conf 
    
Output for MERIS will be in eg ``output/meris/MERIS_WW_1_A_1.fwd_b.plot.y.png`` whereas for MODIS it will be in ``output/modis/MODIS_WW_1_A_1.fwd_b.plot.y.png``

The experiment that demonstrates changing the prior definition is run like ::

eoldas_run.py --conf=config_files/eoldas_config.conf --conf=config_files/meris_single.conf --parameter.limits='[[232,232,1]]' --conf=config_files/modis_single_c.conf 

