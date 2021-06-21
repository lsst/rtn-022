.. image:: https://img.shields.io/badge/rtn--022-lsst.io-brightgreen.svg
   :target: https://rtn-022.lsst.io
.. image:: https://github.com/lsst/rtn-022/workflows/CI/badge.svg
   :target: https://github.com/lsst/rtn-022/actions/

###########################################
Seeing values for LSST strategy simulations
###########################################

RTN-022
=======

The \texttt{opsim4} operations simulation program for the LSST astronomical survey uses a database of seeing values covering the range of times to be simulated. I describe the creation of such a database using Dual Image Motion Monitor (DIMM) data collected at Cerro Pachon from 2004-03-17 to 2019-10-07. In times during which the data overlap, I compare the distribution of DIMM seeing values to the seeing measured in DECam images, taken at a site ~10 km away. Instrumental problems in the DIMM may indicate unreliable measurements, cuts on image quality (as indicated by the measured Strehl ratio) were explored. The DIMM has significant gaps, so I model the data (with and without cuts on Strehl ratio) and generate artificial data in the gaps according to the model. The model consists of a sinusoidal variation with a period of one year, an autoregressive (AR1) model for variations in mean seeing from one night to the next, and another AR1 model for variations on a 5 minute timescale. I create four databases according to this procedure, two based on DIMM data starting 2006-01-01 (with and without a Strehl ratio cut), and two starting 2009-01-01. I then run \texttt{opsim} simulations using each, and an otherwise identical simulation using the default seeing database, and explore the differences.

Links
=====

- Live drafts: https://rtn-022.lsst.io
- GitHub: https://github.com/lsst/rtn-022

Build
=====

This repository includes lsst-texmf_ as a Git submodule.
Clone this repository::

    git clone --recurse-submodules https://github.com/lsst/rtn-022

Compile the PDF::

    make

Clean built files::

    make clean

Updating acronyms
-----------------

A table of the technote's acronyms and their definitions are maintained in the ``acronyms.tex`` file, which is committed as part of this repository.
To update the acronyms table in ``acronyms.tex``::

    make acronyms.tex

*Note: this command requires that this repository was cloned as a submodule.*

The acronyms discovery code scans the LaTeX source for probable acronyms.
You can ensure that certain strings aren't treated as acronyms by adding them to the `skipacronyms.txt <./skipacronyms.txt>`_ file.

The lsst-texmf_ repository centrally maintains definitions for LSST acronyms.
You can also add new acronym definitions, or override the definitions of acronyms, by editing the `myacronyms.txt <./myacronyms.txt>`_ file.

Updating lsst-texmf
-------------------

`lsst-texmf`_ includes BibTeX files, the ``lsstdoc`` class file, and acronym definitions, among other essential tooling for LSST's LaTeX documentation projects.
To update to a newer version of `lsst-texmf`_, you can update the submodule in this repository::

   git submodule update --init --recursive

Commit, then push, the updated submodule.

.. _lsst-texmf: https://github.com/lsst/lsst-texmf
