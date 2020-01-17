# Ultra fast ONT basecaller

This is a very fast basecaseller which can basecall reads as fast as they come
from MinION on ordinary laptop.

## Limitations

* Works only on 64bit linux.
* Only R9.4.1 for now.
* On AMD CPUs it is advised to use: `export MKL_DEBUG_CPU_TYPE=5`
* You need python3 (tested with python 3.6)

## Instalation

* Install Rust (you should already have it ;) )
* Ask for nightly version `rustup default nightly-2019-12-11`
* Clone this repository
* Run `python setup.py`
* Change Rust version to whatever you like

## Running

`deepnano2_caller.py --output out.fasta --directory reads_directory/`

## Benchmarks

Run on subset of 476 reads from [Klebsiela dataset](https://github.com/rrwick/Basecalling-comparison/tree/95bf07476f61cda79e6971f20f48c6ac83e634b3).
MinION produces this amount in apx. 52 seconds assuming maximum throughput (which in reality never
happens, so realistic number is around 70 seconds).

| Basecaller                                  | Time to basecall | 10%-percentile accuracy | Median accuracy | 90%-percentile accuracy |
|---------------------------------------------|------------------|-------------------------|-----------------|-------------------------|
| Guppy 3.3.0 fast, 1 thread XEON E5-2695 v4  | 26m 0s           | 80.4%                   | 87.6%           | 91.8%                   |
| Guppy 3.3.0 fast, 4 threads XEON E5-2695 v4 | 6m 54s           | 80.4%                   | 87.6%           | 91.8%                   |
| DN-blitz, 1 thread XEON E5-2695 v4          | 2m 38s           | 75.5%                   | 84.0%           | 88.7%                   |
| DN-blitz, 4 threads XEON E5-2695 v4         | 41s              | 75.5%                   | 84.0%           | 88.7%                   |
| DN-blitz, 1 thread i7-7700HQ (laptop)       | 1m 50s           | 75.5%                   | 84.0%           | 88.7%                   |
| DN-blitz, 4 threads i7-7700HQ (laptop)      | 34s              | 75.5%                   | 84.0%           | 88.7%                   |
