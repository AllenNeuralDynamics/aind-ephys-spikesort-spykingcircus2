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

The `code/run` script takes the following arguments:

```bash
  --raise-if-fails      Whether to raise an error in case of failure or continue. Default True (raise)
  --apply-motion-correction
                        Whether to apply SpykingCircus2 motion correction. Default: True
  --min-drift-channels MIN_DRIFT_CHANNELS
                        Minimum number of channels to enable SpykingCircus2 motion correction. Default is 96.
  --n-jobs N_JOBS       Number of jobs to use for parallel processing. Default is -1 (all available cores). 
                        It can also be a float between 0 and 1 to use a fraction of available cores
  --params-file PARAMS_FILE
                        Optional json file with parameters
  --params-str PARAMS_STR
                        Optional json string with parameters

```

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

