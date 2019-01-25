# Conda Package Download Data

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a>

This repository describes the conda package download data provided by Anaconda, Inc.  It includes package download counts starting from July 2017 for the following download sources:

* Anaconda Distribution: The default channels hosted on `repo.anaconda.com` (and historically on `repo.continuum.io`)
* Select Anaconda.org channels: Currently this includes:
  - `conda-forge`


## Data Format

The download data is provided as record for every unique combination of:

* `data_source`: `anaconda` for Anaconda distribution and `conda-forge` for the channel on Anaconda.org
* `time`: UTC time, binned by hour
* `pkg_name`: Package name (Ex: `pandas`)
* `pkg_version`: Package version (Ex: `0.23.0`)
* `pkg_platform`: One of `linux-32`, `linux-64`, `osx-64`, `win-32`, `win-64`, `linux-armv7`, `linux-ppcle64`, `linux-aarch64`, or `noarch`
* `pkg_python`: Python version required by the package, if any (Ex: `3.7`)
* `counts`: Number of downloads for this combination of attributs

The storage format is Parquet, one file per day, with SNAPPY compression.  Files are hosted on S3, with the naming convention:

  - `s3://anaconda-package-data/conda/[year]/[month]/[year]-[month]-[day].parquet`


## Known Issues

There are some known gaps in the dataset, and Anaconda.org data doesn't appear in the data set until April 2017.  See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) for more details.


## Updates

This data will be updated approximately monthly.  Note that we may revise historical data if processing issues are discovered, or to add additional data (like new Anaconda.org channels).  We will update the [change log](CHANGE_LOG.MD) when new or revised data is posted.


## License

This dataset is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).  We are offering this data to help the community understand the usage of conda packages, but with no warranty.  If you use this data, please acknowledge Anaconda as the source and link back to this Github repository.


## Feedback

If you have questions or find problems in the data, please open an issue on this repository.  Thanks!
