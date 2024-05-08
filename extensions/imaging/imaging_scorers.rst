.. _imaging_scorers:

Scorers
-------

The two main scorer types availaible in this imaging extension are the:

1. The :ref:`binned_scorer`, and
2. The :ref:`ntuple_scorer`

You can also add :ref:`digitizer` to the scorers to process detected signals, or implement an :ref:`spread_function` into your scorer. These are detailed in the subsections below.

.. _binned_scorer:

Binned scorer
~~~~~~~~~~~~~

The binned scorer accumuates detected signals on a divided volume. The binned scorer is useful for CBCT or Prompt gamma acquisition. You need to set the number of bins on the scoring volume as follows::

	i:Ge/Scorer/XBins     = 512
	i:Ge/Scorer/YBins     = 512

If you are using the ``FlatImager`` parameter as described in the :ref:`flat_panel` section, there is more than one single surface and you thus need to define which surface will be used for scoring. To score on the surface between the scintillator and the photodetector layers, you need to set::

	s:Sc/Scorer/Surface = "Imager/PhotoDetectorScintillatorInterface"


.. _ntuple_scorer:

NTuple scorer
~~~~~~~~~~~~~

The NTuple scorer saves the information of detected signals on each line similar to a PhaseSpace scorer. The NTupble scorer is useful for PET or SPECT image acquisition.


.. _digitizer:

Digitizers
~~~~~~~~~~~

OpenTOPAS has implemented the following digitizers:

* Time resolution
* Dead time
* Energy cutoff
* Sigmoial threshold
* Pulse pile up

You can build a digitizer chain as follows::

	sv:Sc/PETScore/Digitizers   = 3 "EnergyCutoff" "TimeResolution" "DeadTime"

The digitizers will be applied sequentially as defined by the user. Parameters for digitizers can be defined as follow::

	d:Sc/PETScore/Digitizer/TimeResolution                 = 500 ps # Time resolution
	d:Sc/PETScore/Digitizer/DeadTime                       = 10. ms # Dead time
	d:Sc/PETScore/Digitizer/EnergyCutoff/Threshold         = 400 keV # Energy cutoff
	d:Sc/PETScore/Digitizer/EnergyCutoff/Uphold            = 650 keV # Energy cutoff
	d:Sc/PETScore/Digitizer/SigmoidalThresholder/Threshold = 650 keV # Energy cutoff
	u:Sc/PETScore/Digitizer/SigmoidalThresholder/Alpha     = 50.
	u:Sc/PETScore/Digitizer/SigmoidalThresholder/Percent   = 0.9
	d:Sc/PETScore/Digitizer/PulsePileUp/TimingWindow       = 100 ns


.. _spread_function:

Optical Spread Function
~~~~~~~~~~~~~~~~~~~~~~~

In radiation detection, photons can be converted into visible light (a.k.a. optical photons) in order to be detected. However, the interaction between a photon and a scintillating crystal creates tens of thousand optical photons, thus slowing down the simulation. To improve the computational efficiency of the simulation, an optical spread function ([Shi2019]_ and [OConnel2021]_) was proposed as a variance reduction technique. The idea of an OSF is to numerically model the spread of optical photons to follow a Gaussian distribution instead of tracking each optical photon. A scorer using an OSF has been implemented in OpenTOPAS. To utilize the scorer, one needs to measure the OSF seperately then provide it to the simulation::

	#============== Optical spread function parameters ========
	i:Sc/CBCTscorer/HKernelU                       = 5 # size of OSF kernels
	i:Sc/CBCTscorer/HKernelV                       = 5 # size of OSF kernels
	d:Sc/CBCTscorer/InitialEnergy                  = 10.0 keV
	d:Sc/CBCTscorer/EnergyStep                     = 5.0 keV
	dv:Sc/CBCTscorer/DetectorEfficiency/Energies   = 27 10.0 15.0 20.0 25.0 30.0 35.0 40.0 45.0 50.0 55.0 60.0 65.0 70.0 75.0 80.0 85.0 90.0 95.0 100.0 105.0 110.0 115.0 120.0 125.0 130.0 135.0 140.0 keV
	uv:Sc/CBCTscorer/DetectorEfficiency/Efficiency = 27 0.000398 0.026029 0.067879 0.080005 0.069582 0.079304 0.064622 0.069822 0.069503 0.065332 0.059056 0.052028 0.045107 0.038802 0.033204 0.028320 0.024101 0.020590 0.017658 0.015201 0.013128 0.011383 0.009911 0.008660 0.007598 0.006690 0.005907
	s:Sc/CBCTscorer/OSFPath                        = "<path-to-osfs>"
	b:Sc/CBCTscorer/ForceInteraction               = "True"

OpenTOPAS parameters to simulate an OSF can be found in the example parameter files. One can find a detailed description of OSF measuring in a previous publication [Shi2019]_.

References
~~~~~~~~~~

.. [Shi2019] Shi, M. et al., 2019. A novel method for fast image simulation of flat panel detectors. Physics in Medicine & Biology, 64(9), 095019
.. [OConnel2021] O'Connel, J. Bazalova-Carter, M., 2021. fastCAT: Fast cone beam CT (CBCT) simulation. Medical Physics, 48(8), pp.4448-4458
