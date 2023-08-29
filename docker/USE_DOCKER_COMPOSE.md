# Use docker-compose

## Environment

The following steps are compatible at least with these environments.

|-|version|
|:--|:--|
|Ubuntu|20.04.6 LTS.|
|docker|24.0.5|
|nvidia driver|460.106.00|
|cuda|11.2|


## Steps

```bash
$ cd docker/

# Build:
$ docker compose build

# Launch (requires GPUs)
$ docker compose run python /bin/bash
```

Next, go forward to [GETTING_STARTED](GETTING_STARTED.md)!

## Supplement

setup [datasets](datasets)

```bash
$ cd datasets
$ unzip <dataset file>
$ unzip Market-1501-v15.09.15.zip
```

train

```bash
$ python3 tools/train_net.py --config-file ./configs/Market1501/bagtricks_R50.yml MODEL.DEVICE "cuda:0"
```
