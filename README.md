## About

This code is meant to transform Nano Ntuples to plain .npz files.


## Setup

For producing .npz files from .root files:

```
pip install uproot awkward seutils
```

For testing:

```
pip install uproot awkward seutils pytest
```

For reading .npz files only:

```
pip install numpy
```

In any case:

```
pip install https://github.com/boostedsvj/hgcal_npz/archive/main.zip
# To be replaced with something in PyPI once things stabilize.
```


## Usage

For loading an existing .npz file:

```python
>>> import hgcal_npz
>>> event = hgcal_npz.Event.load('seed0_n100_000.npz')
>>> event.metadata
{'version': '0.1', 'rootfile': 'seed0_n100.root', 'i_event': 0, 'npz_file': 'seed0_n100_000.npz'}
>>> event.rechits.keys
['RecHitHGC_x', 'RecHitHGC_y', 'RecHitHGC_z', 'RecHitHGC_energy', 'RecHitHGC_time', 'RecHitHGC_MergedSimClusterBestMatchIdx', 'RecHitHGC_MergedSimClusterBestMatchQual']
>>> event.rechits.array
array([[-4.13478661e+01, -1.60157740e+00,  3.22102753e+02, ...,
        -1.00000000e+00,  1.82500000e+03,  1.00000000e+00],
       [-4.13478661e+01,  8.00788701e-01,  3.22102753e+02, ...,
        -1.00000000e+00,  3.81000000e+02,  1.00000000e+00],
       [-4.13478661e+01,  1.60157740e+00,  3.22102753e+02, ...,
        -1.00000000e+00, -1.00000000e+00,  0.00000000e+00],
       ...,
       [ 1.71291748e+02, -1.67594894e+02, -4.70199493e+02, ...,
         5.02636719e+00,  4.14800000e+03,  1.00000000e+00],
       [ 0.00000000e+00,  0.00000000e+00,  0.00000000e+00, ...,
        -1.00000000e+00, -1.00000000e+00,  0.00000000e+00],
       [ 1.77567642e+02, -1.52328293e+02, -4.95849487e+02, ...,
        -1.00000000e+00,  4.14800000e+03,  1.00000000e+00]])
>>> event.rechits.array.shape
(117294, 7)
```

For producing .npz files from a .root file, there is a command line script:

```bash
hgcal_nano_to_npz seed0_n100.root seed1_n100.root -d outdir --nthreads 2
```

For taking a peek in an .npz file via the command line:

```bash
$ hgcal_npz_ls testdir/seed0_n100_000.npz
<Event
  metadata={
      'i_event': 0,
      'npz_file': 'testdir/seed0_n100_000.npz',
      'rootfile': 'seed0_n100.root',
      'version': '0.1'}
  rechits:
    shape=(117294, 7)
    keys=[
      'RecHitHGC_x',
      'RecHitHGC_y',
      'RecHitHGC_z',
      'RecHitHGC_energy',
      'RecHitHGC_time',
      'RecHitHGC_MergedSimClusterBestMatchIdx',
      'RecHitHGC_MergedSimClusterBestMatchQual']
  simtracks:
    shape=(19, 13)
    keys=[
      'SimTrack_pdgId',
      'SimTrack_trackId',
      'SimTrack_boundaryMomentum_eta',
      'SimTrack_boundaryMomentum_phi',
      'SimTrack_boundaryMomentum_pt',
      'SimTrack_boundaryPos_x',
      'SimTrack_boundaryPos_y',
      'SimTrack_boundaryPos_z',
      'SimTrack_eta',
      'SimTrack_phi',
      'SimTrack_pt',
      'SimTrack_trackIdAtBoundary',
      'SimTrack_crossedBoundary']
  simclusters:
    shape=(4567, 5)
    keys=[
      'MergedSimCluster_boundaryEnergy',
      'MergedSimCluster_boundaryP4',
      'MergedSimCluster_recEnergy',
      'MergedSimCluster_pdgId',
      'MergedSimCluster_trackIdAtBoundary']
```