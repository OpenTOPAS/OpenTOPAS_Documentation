Welcome to the OpenTOPAS documentation!
=======================================

OpenTOPAS_ wraps and extends the `Geant4 Simulation Toolkit`_ to provide an easier-to-use application for the medical physicist. OpenTOPAS's unique parameter control system lets you assemble and control a rich library of simulation objects (geometry components, particle sources, scorers, etc.) with no need to write C++ code.

Advanced users remain free to implement their own simulation objects in C++ code, and add them to OpenTOPAS via an :ref:`extension mechanism <extensions>`. While user-written objects benefit from underlying functionality of TOPAS base classes and the TOPAS parameter control system used in OpenTOPAS, they can exploit the full flexibility of Geant4.

To discover the Geant4 version used by a specific version of OpenTOPAS, please consult the :ref:`version` section.

.. note:: A PDF version of the documentation is found by clicking the "Read the Docs" panel in the bottom-right corner of the website.


.. toctree::
    :hidden:
    :maxdepth: 1
    :caption: Getting Started

    getting-started/install
    getting-started/authors
    getting-started/citation
    getting-started/users
    getting-started/G4_version


.. toctree::
    :hidden:
    :maxdepth: 1
    :caption: Simulation Control

    parameters/intro


.. toctree::
    :hidden:
    :maxdepth: 1
    :caption: Example Parameter Files

    examples-docs/Basic/index
    examples-docs/Brachytherapy/index
    examples-docs/Graphics/index
    examples-docs/MVLinac/index
    examples-docs/Nozzle/index
    examples-docs/Optical/index
    examples-docs/Outcome/index
    examples-docs/Patient/index
    examples-docs/PhaseSpace/index
    examples-docs/Scoring/index
    examples-docs/SpecialComponents/index
    examples-docs/TimeFeature/index
    examples-docs/UCSFETF/index
    examples-docs/VarianceReduction/index
 

.. toctree::
    :hidden:
    :maxdepth: 1
    :caption: How to Extend OpenTOPAS

    extension-docs/intro
 

.. toctree::
    :hidden:
    :maxdepth: 1
    :caption: Provided Extensions

    extensions/imaging/index

.. _OpenTOPAS: https://github.com/OpenTOPAS/OpenTOPAS
.. _Geant4 Simulation Toolkit: https://geant4.web.cern.ch

