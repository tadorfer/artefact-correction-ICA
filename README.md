# Artefact Correction with ICA

This repository contains the notebook referenced in my [Medium post](https://medium.com/@thomas.a.dorfer/artefact-correction-with-ica-53afb63ad300) on ICA-based artefact correction.

The EEG data used in this notebook, `eeg.csv`, was originally loaded into Python using the [MNE package](https://mne.tools/stable/index.html). Assuming the raw EEG data file is named `eeg.vhdr` (Brain Products), the corresponding code to convert the .vhdr file to .csv is as follows:

```python
import mne
import pandas as pd

# load data into MNE
raw = mne.io.read_raw_brainvision('eeg.vhdr')

# set channel montage
montage = mne.channels.make_standard_montage('standard_1020')
raw.set_montage(montage)

# get channel names
channels = raw.info.ch_names

# get the data in shape (samples, channels)
eeg = raw.get_data().T

# construct and save Pandas DataFrame as .csv
df = pd.DataFrame(eeg, columns=channels)
df.to_csv('eeg.csv', index=False)

```

**Note:** This does not include any preprocessing steps such as average referencing or signal filtering.
