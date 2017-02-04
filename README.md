# PyWorldVocoder<br/>A Python wrapper for World Vocoder

Morise's World Vocoder is a fast and high-quality vocoder.
World Vocoder parameterizes speech into three components:

  5. Pitch (fundamental frequency, F0) contour  
  2. smoothed spectrogram  
  3. aperiodicity  

It can also resynthesize speech using these features.

For more information, please visit Morise's Github repository:  
  https://github.com/mmorise/World  
  <br/>
  And the official website of World Vocoder:<br/>
  http://ml.cs.yamanashi.ac.jp/world/english/


## I. APIs

### Vocoder Functions
```python
import pyworld as pw
pyDioOpt = pw.pyDioOption()
_f0, t = pw.dio(x, fs)    # raw pitch extractor
f0 = pw.stonemask(x, _f0, t, fs)  # pitch refinement
sp = pw.cheaptrick(x, f0, t, fs)  # extract smoothed spectrogram
ap = pw.d4c(x, f0, t, fs)         # extract aperiodicity
y = pw.synthesize(f0, sp, ap, fs, pyDioOpt.option['frame_period'])
```


### Utility
```python
# Convert speech into features (using default options)
f0, sp, ap, pyDioOpt = pw.wav2world(x, fs)
```

<br/>

## II. Installation
### Environment
Linux Ubuntu 14.04 <br/>
Python 2.7.6 on <br/>
Cython 0.24 (or later versions; required)
Matplotlib (optional; for demo.py only)

### Installation procedures
```bash
git clone https://github.com/JeremyCCHsu/Python-Wrapper-for-World-Vocoder.git
cd Python-Wrapper-for-World-Vocoder
bash download_vocoder.sh
```
It will automatically `git clone` Morise's World Vocoder (C++ version).  
Then you can choose from the following installation options.


### Installation Mode
9. If you want to "install" this package, try <br/>
  `python setup.py install`  
  (add `--user` if you don't have root access)
0. If you just want to try out some experiments, execute  
  `python setup.py build_ext --inplace` <br/>
  Then you can use PyWorld from this directory.<br/>
  You can also copy the resulting **pyworld.so** file to  
  `~/.local/lib/python2.7/site-packages` <br/>
  so that you can use it everywhere like an installed package.


### Validation
You can validate installation by running     
`python demo.py`  
to see if you get results in `test/` direcotry.

<br/>

## Troubleshooting
0. Upgrade your Cython version to 0.24.<br/>
   (I failed to build it on Cython 0.20.1post0)<br/>
   It'll require you to download Cython form http://cython.org/ <br/>
   Unzip it, and `python setup.py install` it.<br/>
   (I tried `pip install Cython` but the upgrade didn't seem correct)<br/>
   (Again, add `--user` if you don't have root access.)  

1. The following code might be needed in some configurations:
  ```python
  import matplotlib  
  matplotlib.use('Agg')
  ```

<br/>

## Note:
1. This wrapper is an updated version of sotelo's "world.py"<br/>
  https://github.com/sotelo/world.py

## TODO List

- [ ] Realtime synthesizer
