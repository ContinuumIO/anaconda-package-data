# Conda Package Download Data

This repository describes the conda package download data provided by Anaconda, Inc.  It includes package download counts starting from July 2017 for the following download sources:

* Anaconda Distribution: The default channels hosted on `repo.anaconda.com` (and historically on `repo.continuum.io`)
* Select Anaconda.org channels: Currently this includes:
  - `conda-forge`


## Data Format

The download data is provided as record for every unique combination of:

* Time, binned by hour (UTC)
* Package name (Ex: `pandas`)
* Package version (Ex: `0.23.0`)
* Package platform: `linux-32`, `linux-64`, `osx-64`, `win-32`, `win-64`, `linux-armv7`, `linux-ppcle64`, `linux-aarch64`, or `noarch`
* Python version (if Python is a dependency)
* Anaconda.org Channel (NA for Anaconda Distribution)
* Package download count

The storage format is Parquet, one file per day, with SNAPPY compression.  Files are hosted on S3, with the naming convention:

  - `s3://anaconda-package-data/conda/[year]/[month]/[year]-[month]-[day].parquet`


## Updates

This data will be updated approximately monthly.  Note that we may revise historical data if processing issues are discovered, or to add additional data (like new Anaconda.org channels).  We will update the [CHANGE_LOG] when new or revised data is posted.


## License

This data is provided as-is, with no warranty.  See [LICENSE.txt](LICENSE.txt) for more information.


## Feedback

If you have questions or find problems in the data, please open an issue on this repository.  Thanks!
