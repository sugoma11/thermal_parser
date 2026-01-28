# FLIR/DJI IR Camera Data Parser, Python Version

Parser infrared camera data as `NumPy` data.

![image](./images/image.jpg)

## Installation

0. This package is managed by uv. [Uv installation](https://docs.astral.sh/uv/getting-started/installation/#__tabbed_1_1).

1. User installation (create venv before):
```bash
uv pip install https://github.com/sugoma11/thermal_parser.git;
# pip install https://github.com/sugoma11/thermal_parser.git # if you prefer just pip
```

2. For development:
```bash
git clone git@github.com:sugoma11/thermal_parser.git;
cd thermal_parser;
uv sync;
# pip install -e . # if you prefer just pip
```

## Quick start
See the [Jupyter Notebook examples](./quick_start.ipynb).

## CLI Usage

```bash
# Process single file
uv run thermal-parser images/DJI_H20T.jpg

# Process directory with 4 workers
uv run thermal-parser images/M2EA -w 4

# Output as numpy, int16 dtype
uv run thermal-parser images/DJI_H20T.jpg -f npy -d int16

# See all options
uv run thermal-parser --help
```

## Python API

```python
import numpy as np
from thermal_parser import Thermal

thermal = Thermal(dtype=np.float32)
temperature = thermal.parse(filepath_image='images/DJI_H20T.jpg')
assert isinstance(temperature, np.ndarray)
```

## Supported IR Camera

FLIR R-JPEG Camera Model

* FLIR
* FLIR AX8
* FLIR B60
* FLIR E40
* FLIR T640

DJI R-JPEG Camera Model

* DJI H20T
* DJI XT2
* DJI XTR
* DJI XTS / 禅思 Zenmuse XT S

DJI R-JPEG Camera Model DTAT3.0

* DJI M2EA / DJI MAVIC2-ENTERPRISE-ADVANCED / "御"2 行业进阶版
* DJI H20N / 禅思 H20N
* DJI M3T / DJI MAVIC3 / DJI Mavic 3 行业系列
* DJI M30T / 经纬 M30 系列
* DJI M3TD / 大疆机场 2
* DJI H30T / 禅思 H30 系列
* DJI M4T / DJI Matrice 4 系列

## References

* [DJI Thermal SDK](https://www.dji.com/cn/downloads/softwares/dji-thermal-sdk) The DJI Thermal SDK enables you to process R-JPEG (Radiometric JPEG) images which were captured by DJI infrared camera products.
* [Thermal Image Analysis](https://github.com/detecttechnologies/Thermal-Image-Analysis) A tool for analyzing and annotating thermal images.
* [Base codes for Thermography](https://github.com/detecttechnologies/thermal_base) A python package for decoding and common processing for thermographs / thermograms
* [thermography](https://github.com/cdeldon/thermography) This repository contains the implementation of a feasibility study for automatic detection of defected solar panel modules.
* [DJI Thermal Analysis Tool 3](https://www.dji.com/global/downloads/softwares/dji-dtat3) DJI Infrared Thermal Analysis Tool 3 is mainly used for analyzing and processing infrared photos. It can help you analyze the state of the object by obtaining temperature information of key positions of the photographed object.

# Docker
```
sudo docker build -t dji-thermal .

mac
sudo docker run --rm -it --name dji-thermal -v $(pwd):/usr/src/app dji-thermal:latest

sudo docker run --rm -it --name dji-thermal -v $(pwd):/usr/src/app dji-thermal:latest python app.py


windows
sudo docker run --rm -it --name dji-thermal -v ${pwd}:/usr/src/app dji-thermal:latest

```