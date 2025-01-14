# Conda Package Download Data

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a>

This repository describes the conda package download data provided by Anaconda, Inc.  It includes package download counts starting from Jan. 2017 for the following download sources:

* Anaconda Distribution: The default channels hosted on `repo.anaconda.com` (and historically on `repo.continuum.io`)
* Select Anaconda.org channels: Currently this includes `conda-forge` and `bioconda`.

## Quickstart

From the root folder, run:

```
conda env create --file binder/environment.yml
conda activate package-data-example
jupyter notebook
```
Then double-click on the anaconda_package_data_quick notebook and follow the instructions there.


## Data Format

The download data is provided as record for every unique combination of:

* `data_source`: `anaconda` for Anaconda distribution, `conda-forge` for the conda-forge channel on Anaconda.org, and `bioconda` for the bioconda channel on Anaconda.org.
* `time`: UTC time, binned by hour
* `pkg_name`: Package name (Ex: `pandas`)
* `pkg_version`: Package version (Ex: `0.23.0`)
* `pkg_platform`: One of `linux-32`, `linux-64`, `osx-64`, `win-32`, `win-64`, `linux-armv7`, `linux-ppcle64`, `linux-aarch64`, or `noarch`
* `pkg_python`: Python version required by the package, if any (Ex: `3.7`)
* `counts`: Number of downloads for this combination of attributs

The storage format is Parquet, one file per day, with SNAPPY compression.  Files are hosted on S3, with the naming convention:

  - `s3://anaconda-package-data/conda/hourly/[year]/[month]/[year]-[month]-[day].parquet`


## Data Catalog

To simplify using the dataset, we have also created an [Intake](https://intake.readthedocs.io/en/latest/) catalog file, which you can load either directly from the repository if you have the `intake`, `intake-parquet`, and `python-snappy` packages installed:

``` python
import intake

cat = intake.Catalog('https://raw.githubusercontent.com/ContinuumIO/anaconda-package-data/master/catalog/anaconda_package_data.yaml')
monthly = cat.anaconda_package_data_by_month(year=2019, month=12).to_dask()
```

Or you can install the data package directly with conda, which will also fetch the required dependencies:

```
conda install -c intake anaconda-package-data
```

And then the data source will appear in the global catalog of your conda environment:

``` python
import intake

monthly = intake.cat.anaconda_package_data_by_month(year=2019, month=12).to_dask()
```

To minimize bandwidth usage, these catalogs are configured so that Intake will cache data locally to your system on first use.


## Known Issues

There are some known gaps in the dataset, and Anaconda.org data doesn't appear in the data set until April 2017.  See [KNOWN_ISSUES.md](KNOWN_ISSUES.md) for more details.


## Updates

This data will be updated approximately monthly.  Note that we may revise historical data if processing issues are discovered, or to add additional data (like new Anaconda.org channels).  We will update the [change log](CHANGE_LOG.md) when new or revised data is posted.


## License

This dataset is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).  We are offering this data to help the community understand the usage of conda packages, but with no warranty.  If you use this data, please acknowledge Anaconda as the source and link back to this Github repository.


## Feedback

If you have questions or find problems in the data, please open an issue on this repository.  Thanks!
