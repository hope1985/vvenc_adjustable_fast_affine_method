# VVenC

![VVenC Logo](https://github.com/fraunhoferhhi/vvenc/wiki/img/VVenC_RGB_small.png)

VVenC, the Fraunhofer Versatile Video Encoder, is a fast and efficient software H.266/VVC encoder implementation with the following main features:
- Easy to use encoder implementation with five predefined quality/speed presets;
- Perceptual optimization to improve subjective video quality, based on the XPSNR visual model;
- Extensive frame-level and task-based parallelization with very good scaling;
- Frame-level single-pass and two-pass rate control supporting variable bit-rate (VBR) encoding;
- Expert mode encoder interface available, allowing fine-grained control of the encoding process.

## Information

See the [Wiki-Page](https://github.com/fraunhoferhhi/vvenc/wiki) for more information:

* [Build information](https://github.com/fraunhoferhhi/vvenc/wiki/Build)
* [Usage documentation](https://github.com/fraunhoferhhi/vvenc/wiki/Usage)
* [VVenC performance](https://github.com/fraunhoferhhi/vvenc/wiki/Encoder-Performance)
* [License](https://github.com/fraunhoferhhi/vvenc/wiki/License)
* [Publications](https://github.com/fraunhoferhhi/vvenc/wiki/Publications)
* [Version history](https://github.com/fraunhoferhhi/vvenc/wiki/Changelog)

## Adjustable Fast Affine Decision Method

This is the modified version of VVenC encoder with the fast affine decision method proposed in the paper below:

[H. Pejman*, S. Coulombe*, C. Vazquez*, M. Jamali° and A. Vakili°, "An Adjustable Fast Decision Method for Affine Motion Estimation in VVC," ICIP, Kuala Lumpur, Malaysia, 2023, pp. 2695-2699, doi: 10.1109/ICIP49359.2023.10222750.](https://ieeexplore.ieee.org/document/10222750)

*École de technologie supérieure, °Summit Tech Multimedia

## Modifications

To add the fast affine decision method to the VVenC encoder, the following files have been modified:

-	include\vvenc\VVencCfg.h
-	source\Lib\vvenc\VVencCfg.cpp
-	source\Lib\EncoderLib\InterSearch.cpp
-	source\Lib\apputil\VVEncAppCfg.h

All the modified/Added codes are tagged between two comment lines as follows:

```
// =========== FAST_AFFINE, H.Pejman et al., ICIP2023 =============
                    Added/Modified codes
// =========== FAST_AFFINE, H.Pejman et al., ICIP2023 =============
```

The ```ENABLE_AFFINE_THR``` macro is defined in ```include\vvenc\vvencCfg.h``` file to enable the fast affine method (removing this macro disables all codes related to the fast affine method). 

The ```-aft``` parameter is added to VVenC to determine the threshold value of the fast affine method. For example, the line below runs vvencFFapp with a threshold value of 0.6:

```
vvencFFapp -c randomaccess_medium.cfg  -i <input>  -aft 0.6  --affine 1  ...
```

## Build

VVenC uses CMake to describe and manage the build process. A working [CMake](https://cmake.org/) installation is required to build the software. In the following, the basic build steps are described. Please refer to the [Wiki](https://github.com/fraunhoferhhi/vvenc/wiki/Build) for the description of all build options.

### How to build using CMake?

To build using CMake, create a `build` directory and generate the project:

```sh
mkdir build
cd build
cmake .. <build options>
```

To actually build the project, run the following after completing project generation:

```sh
cmake --build .
```

For multi-configuration projects (e.g. Visual Studio or Xcode) specify `--config Release` to build the release configuration.

### How to build using GNU Make?

On top of the CMake build system, convinence Makefile is provided to simplify the build process. To build using GNU Make please run the following:

```sh
make install-release <options>
```

Other supported build targets include `configure`, `release`, `debug`, `relwithdebinfo`, `test`,  and `clean`. Refer to the Wiki for a full list of supported features.

## Citing

Please use the following citation when referencing VVenC in literature:

```bibtex
@InProceedings{VVenC,
  author    = {Wieckowski, Adam and Brandenburg, Jens and Hinz, Tobias and Bartnik, Christian and George, Valeri and Hege, Gabriel and Helmrich, Christian and Henkel, Anastasia and Lehmann, Christian and Stoffers, Christian and Zupancic, Ivan and Bross, Benjamin and Marpe, Detlev},
  booktitle = {Proc. IEEE International Conference on Multimedia Expo Workshops (ICMEW)},
  date      = {2021},
  title     = {VVenC: An Open And Optimized VVC Encoder Implementation},
  doi       = {10.1109/ICMEW53276.2021.9455944},
  pages     = {1-2},
}
```

## Contributing

Feel free to contribute. To do so:

* Fork the current-most state of the master branch
* Apply the desired changes
* For non-trivial contributions, add your name to [AUTHORS.md](./AUTHORS.md)
* Create a pull-request to the upstream repository

## License

Please see [LICENSE.txt](./LICENSE.txt) file for the terms of use of the contents of this repository.

For more information, please contact: vvc@hhi.fraunhofer.de

**Copyright (c) 2019-2024, Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V. & The VVenC Authors.**

**All rights reserved.**

**VVenC® is a registered trademark of the Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V.**
