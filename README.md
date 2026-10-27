# Spike sorting with Spyking-CIRCUS2 for AIND ephys pipeline
## aind-ephys-spikesort-spykingcircus2


### Description

This capsule is designed to spike sort ephys data using SpykingCircus2 for the AIND pipeline.

This capsule spike sorts preprocessed ephys stream and applies a minimal curation to:

- remove empty units
- remove excess spikes (falling beyond the end of the recording)


### Inputs

The `data/` folder must include the output of the [aind-ephys-preprocessing](https://github.com/AllenNeuralDynamics/aind-ephys-preprocessing), containing 
the `data/preprocessed_{recording_name}` folder.

### Parameters

Parameters are read from a `params.json` file that must be in the root folder of the capsule (next to `code/`, i.e. `../params.json` from `code/`), using the `spikesorting.spykingcircus2` section (`skip_motion_correction`, `min_drift_channels`, `raise_if_fails`, `n_jobs`, `job_kwargs`, `sorter`, ...) and the optional top-level `logging` section.

A list of spike sorting parameters can be found in the `code/params.json`:

```json
{
    "job_kwargs": {
        "chunk_duration": "1s",
        "progress_bar": false
    },
    "sorter": {
        "general": {"ms_before": 2, "ms_after": 2, "radius_um": 100},
        "sparsity": {"method": "snr", "amplitude_mode": "peak_to_peak", "threshold": 0.25},
        "filtering": {"freq_min": 150, "freq_max": 7000, "ftype": "bessel", "filter_order": 2},
        "detection": {"peak_sign": "neg", "detect_threshold": 4},
        "selection": {
            "method": "uniform",
            "n_peaks_per_channel": 5000,
            "min_n_peaks": 100000,
            "select_per_channel": false,
            "seed": 42
        },
        "apply_motion_correction": true,
        "motion_correction": {"preset": "dredge_fast"},
        "merging": {
            "similarity_kwargs": {"method": "cosine", "support": "union", "max_lag_ms": 0.2},
            "correlograms_kwargs": {},
            "auto_merge": {
                "min_spikes": 10,
                "corr_diff_thresh": 0.25
            }
        },
        "clustering": {"legacy": true},
        "matching": {"method": "wobble"},
        "apply_preprocessing": true,
        "matched_filtering": true,
        "cache_preprocessing": {"mode": "no-cache", "memory_limit": 0.5, "delete_cache": true},
        "multi_units_only": false,
        "job_kwargs": {"n_jobs": 0.8},
        "debug": false
    }
}
```

### Output

The output of this capsule is the following:

- `results/spikesorted_{recording_name}` folder, containing the spike sorted data saved by SpikeInterface and the spike sorting log
- `results/data_process_spikesorting_{recording_name}.json` file, a JSON file containing a `DataProcess` object from the [aind-data-schema](https://aind-data-schema.readthedocs.io/en/stable/) package.

