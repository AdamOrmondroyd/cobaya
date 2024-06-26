CMB from Planck
==================

Family of Planck CMB likelihoods. Contains interfaces to the official 2018 ``clik`` code and some
native ones, including more recent NPIPE (PR4) results that can be run without clik.
You can find a description of the different original likelihoods in the
`Planck wiki <https://wiki.cosmos.esa.int/planck-legacy-archive/index.php/CMB_spectrum_%26_Likelihood_Code>`_.

.. |br| raw:: html

   <br />

The Planck 2018 baseline likelihoods defined here are:

- ``planck_2018_lowl.TT``: low-:math:`\ell` temperature (native python implementation)
- ``planck_2018_lowl.EE``: low-:math:`\ell` EE polarization (native python implementation)
- ``planck_2018_lowl.[TT|EE]_clik``: original clik versions of the above
- ``planck_2018_highl_plik.[TT|TTTEEE]``: ``plikHM`` high-:math:`\ell` temperature|temperature+polarization
- ``planck_2018_highl_plik.[TT|TTTEEE]_unbinned``: unbinned versions of the previous ones
- ``planck_2018_highl_plik.[TT|TTTEEE]_lite``: faster nuisance-marginalized versions of the previous (binned) ones
- ``planck_2018_highl_plik.[TT|TTTEEE]_lite_native``: Python native versions of the nuisance-marginalizes ones  (more customizable)
- ``planck_2018_highl_CamSpec.[TT|TTTEEE][_native]``: ``clik`` and native Python versions of the alternative high-:math:`\ell` ``CamSpec`` likelihoods.
- ``planck_2018_lensing.clik``: lensing temperature+polarisation-based; official ``clik`` code.
- ``planck_2018_lensing.native``: lensing temperature+polarisation-based; native Python version (more customizable)
- ``planck_2018_lensing.CMBMarged``: CMB-marginalized, temperature+polarisation-based lensing likelihood; native Python version (more customizable). Do not combine with any of the ones above!

Other more recent Planck likelihoods are:

- ``planck_NPIPE_highl_CamSpec.[TT|TE|EE|TTEE|TTTEEE]``: latest native (bundled) python NPIPE (PR4) CamSpec high-:math:`\ell` likelihoods
- ``planck_2020_lollipop.[lowlE|lowlB|lowlEB]``: latest python NPIPE (PR4) Lollipop low-:math:`\ell` likelihoods. pip install from `GitHub <https://github.com/planck-npipe/lollipop>`_
- ``planck_2020_hillipop.[TT|TE|EE|TTTEEE]``: latest python NPIPE (PR4) Hillipop high-:math:`\ell` likelihoods. pip install from `GitHub <https://github.com/planck-npipe/hillipop>`_
- ``planckpr4lensing.[PlanckPR4Lensing|PlanckPR4LensingMarged]``: NPIPE lensing; pip install from `GitHub <https://github.com/carronj/planck_PR4_lensing>`_
- ``planck_2018_highl_CamSpec2021.[TT|TTTEEE]``: native Python versions of high-:math:`\ell` ``CamSpec`` likelihoods (from `arXiv 1910.00483 <https://arxiv.org/abs/1910.00483>`_).
- ``planck_2018_lowl.EE_sroll2``: low-:math:`\ell` EE polarization from 2019 Sroll2 analysis (native python)

The combination of planck_2018_lowl.TT, planck_2018_lowl.EE, planck_NPIPE_highl_CamSpec.TTTEEE, planckpr4lensing, planck_2020_hillipop and planck_2020_lollipop can be run using the pure python without installing the 2018 clik likelihood package.

.. note::

   **If you use any of these likelihoods, please cite and other relevant papers:**
   |br|
   Planck Collaboration, `Planck 2018 results. V. CMB power spectra and likelihoods`
   `(arXiv:1907.12875) <https://arxiv.org/abs/1907.12875>`_
   |br|
   Planck Collaboration, `Planck 2018 results. VIII. Gravitational lensing`
   `(arXiv:1807.06210) <https://arxiv.org/abs/1807.06210>`_


The Planck 2015 likelihoods defined here are:

- ``planck_2015_lowl``
- ``planck_2015_lowTEB``
- ``planck_2015_plikHM_TT``
- ``planck_2015_plikHM_TT_unbinned``
- ``planck_2015_plikHM_TTTEEE``
- ``planck_2015_plikHM_TTTEEE_unbinned``
- ``planck_2015_lensing``
- ``planck_2015_lensing_cmblikes``
  (a native non-clik, more customizable version of the previous clik-wrapped one)

.. note::

   **If you use any of these likelihoods, please cite them as:**
   |br|
   **2015**:  N. Aghanim et al,
   `Planck 2015 results. XI. CMB power spectra, likelihoods, and robustness of parameters`
   `(arXiv:1507.02704) <https://arxiv.org/abs/1507.02704>`_


.. warning::

   The Planck 2015 likelihoods have been superseded by the 2018 release, and will
   eventually be deprecated.

.. warning::

   Some likelihoods cannot be instantiated more than once, or some particular two at the same time.
   This should have no consequences when calling ``cobaya-run`` from the shell, but will impede running
   a sampler or defining a model more than once per Python interpreter session.


Usage
-----

To use any of the Planck likelihoods, you simply need to mention them in the
``likelihood`` block, or add them using the :doc:`input generator <cosmo_basic_runs>`.

The corresponding nuisance parameters will be added automatically,
so you don't have to care about listing them in the ``params`` block.

The nuisance parameters and their default priors can be obtained as explained in :ref:`citations`.


Installation
------------

This likelihoods can be installed automatically as explained in :doc:`installation_cosmo`.
If you are following the instructions there (you should!), you don't need to read the rest
of this section.

.. note::

   For the 2018 clik likelihoods, by default the ``gfortran`` compiler will be used,
   and the ``cfitsio`` library will be downloaded and compiled automatically.

   If the installation fails, make sure that the packages ``liblapack3`` and
   ``liblapack-dev`` are installed in the system (in Debian/Ubuntu, simply do
   ``sudo apt install liblapack3 liblapack-dev``).

   If that did not solve the issue, check out specific instructions for some systems in the
   ``readme.md`` file in the folder ``[packages_path]/code/planck/code/plc_3.0/plc-3.01``.

   If you want to re-compile the Planck likelihood to your liking (e.g. with MKL), simply
   go into the chosen external packages installation folder and re-run the ``python waf configure``
   and ``python waf install`` with the desired options,
   substituting ``python`` by the Python of choice in your system.

However, if you wish to install it manually or have a previous installation already in
your system, simply make sure that ``clik`` can be imported from anywhere,
and give **absolute** paths for each *clik file*, e.g.:

.. code-block:: yaml

   likelihood:
     planck_2018_lowl.TT_clik:
       clik_file: /your/path/to/plc_3.0/low_l/commander/commander_dx12_v3_2_29.clik
     planck_2018_highl_plik.TTTEEE:
       clik_file: /your/path/to/plc_3.0/hi_l/plik/plik_rd12_HM_v22b_TTTEEE.clik


Manual installation of the Planck 2018 likelihoods
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Assuming you are installing all your likelihoods under ``/path/to/likelihoods``:

.. code:: bash

   $ cd /path/to/likelihoods
   $ mkdir planck_2018
   $ cd planck_2018
   $ wget "https://pla.esac.esa.int/pla-sl/data-action?COSMOLOGY.COSMOLOGY_OID=151912"
   $ tar xvjf "data-action?COSMOLOGY.COSMOLOGY_OID=151912"
   $ rm "data-action?COSMOLOGY.COSMOLOGY_OID=151912"
   $ cd code/plc_3.0/plc-3.01
   $ python waf configure  # [options]

If the last step failed, try adding the option ``--install_all_deps``.
It it doesn't solve it, follow the instructions in the ``readme.md``
file in the ``plc_3.0`` folder.

If you have Intel's compiler and Math Kernel Library (MKL), you may want to also add the
option ``--lapack_mkl=${MKLROOT}`` in the last line to make use of it.

If ``python waf configure`` ended successfully run ``python waf install``
in the same folder. You do **not** need to run ``clik_profile.sh``, as advised.

Now, download the required likelihood files from the
`Planck Legacy Archive <https://pla.esac.esa.int/pla/#cosmology>`_ (Europe) or the
`NASA/IPAC Archive <https://irsa.ipac.caltech.edu/data/Planck/release_2/software/>`_ (US, **outdated!**).

For instance, if you want to reproduce the baseline Planck 2018 results,
download the file ``COM_Likelihood_Data-baseline_R3.00.tar.gz``
from any of the two links above, and decompress it under the ``planck_2018`` folder
that you created above.

Finally, download and decompress in the ``planck_2018`` folder the last release at
`this repo <https://github.com/CobayaSampler/planck_supp_data_and_covmats/releases>`_.


Interface for official ``clik`` code
------------------------------------

.. automodule:: cobaya.likelihoods.base_classes.planck_clik
   :noindex:

Native ``CamSpec`` version
--------------------------

.. automodule:: cobaya.likelihoods.base_classes.planck_2018_CamSpec_python
   :noindex:

Native ``lite`` version
-----------------------

.. automodule:: cobaya.likelihoods.base_classes.planck_pliklite
   :noindex:
