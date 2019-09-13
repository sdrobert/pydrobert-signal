[![Build Status](https://travis-ci.com/sdrobert/pydrobert-speech.svg?branch=master)](https://travis-ci.com/sdrobert/pydrobert-speech)
[![Documentation Status](https://readthedocs.org/projects/pydrobert-speech/badge/?version=latest)](https://pydrobert-speech.readthedocs.io/en/latest/?badge=latest)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# pydrobert-speech

This pure-python library allows for flexible computation of speech features.

For example, given feature configuration called `fbanks.json`:

``` json
{
  "name": "stft",
  "bank": "fbank",
  "frame_length_ms": 25,
  "include_energy": true,
  "pad_to_nearest_power_of_two": true,
  "window_function": "hanning",
  "use_power": true
}
```

You can compute triangular, overlapping filters like
[Kaldi](http://kaldi-asr.org/) or [HTK](http://htk.eng.cam.ac.uk/) with the
commands

``` python
import json
from pydrobert.speech import *
# get the feature computer ready
params = json.load(open('fbank.json'))
computer = util.alias_factory_subclass_from_arg(compute.FrameComputer, params)
# assume "signal" is a numpy float array
feats = computer.compute_full(signal)
```

If you plan on using a [PyTorch](https://pytorch.org) `DataLoader` or Kaldi
tables in your ASR pipeline, you can compute all a corpus' features by
using the commmands `signals-to-torch-feat-dir` (requires *pytorch* package)
or `compute-feats-from-kaldi-tables` (requires *pydrobert-kaldi* package).

This package can compute much more than f-banks, with many different
permutations. Consult the documentation for a more in-depth discussion of how
to use it.

## Documentation

- [Latest](https://pydrobert-speech.readthedocs.io/en/latest/)
- [Stable](https://pydrobert-speech.readthedocs.io/en/stable/)

## Installation

_pydrobert-speech_ is available via both PyPI and Conda.

``` sh
conda install -c sdrobert pydrobert-speech
pip install pydrobert-speech
pip install git+https://github.com/sdrobert/pydrobert-speech # bleeding edge
```

## Licensing and How to Cite

Portions of `util.read_signal` were adapted from the
[NIST sph2pipe program]<https://www.ldc.upenn.edu/language-resources/tools/sphere-conversion-tools>.
License information can be found in `LICENSE_sph2pipe`. As of now, we do not
use any of the code from `shorten_x.c`.

Please see the [pydrobert page](https://github.com/sdrobert/pydrobert) for more
details on how to cite this package.
