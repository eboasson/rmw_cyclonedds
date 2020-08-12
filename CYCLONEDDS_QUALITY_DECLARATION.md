This document is a declaration of software quality for the `CycloneDDS` external dependency imported by the rmw\_cyclonedds package, based on the guidelines in [REP-2004](https://www.ros.org/reps/rep-2004.html).

# `CycloneDDS` Quality Declaration

This quality declaration claims that `CycloneDDS` is in the **Quality Level 3** category.

The `CycloneDDS` project meets a substantial number of the criteria stated for software quality.
The developers have taken many steps to ensure that `CycloneDDS` is a software product which can be relied upon, however there is a significant lack of documentation regarding the interpretation of versions, features, and testing.
Even minimal investments in these areas would contribute to the quality of the project, and could increase the level category for `CycloneDDS` in a subsequent review.

Below are the rationales, notes, and caveats for this claim, organized by each requirement listed in the [Package Requirements for Quality Level 4 in REP-2004](https://www.ros.org/reps/rep-2004.html).

## Version Policy [1]

### Version Scheme [1.i]

`CycloneDDS` versioning follows the standard semantic versioning except that major version 0 is also considered stable. `CycloneDDS` was already a stable code base when it was contributed to [Eclipse Foundation](https://eclipse.org)

* MAJOR version when you make incompatible API changes.
* MINOR version when you add functionality in a backwards compatible manner. MINOR IS source compatible (we strive to maintain binary compatibility as well).
* PATCH version when you make backwards compatible bug fixes. PATCH is binary compatible.

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.
This is what has been the case and we see no reason not to follow this going forward.
Thus far, there’s been no MINOR release that has broken binary compatibility. And note that this only holds for the stable interface. Along with bumping MAJOR to 1, this policy will be reconsidered and it may be decided to guarantee binary compatibility for MINOR versions is as well.

The CMake sources configure the compatibility mode to [`SameMajorVersion`](https://cmake.org/cmake/help/latest/module/CMakePackageConfigHelpers.html#generating-a-package-version-file), indicating that breaking changes are accompanied by a change to the `MAJOR` version part.
There is no explicit policy regarding versioning in the documentation for `CycloneDDS`, however there is some information in the [Releases section](https://www.eclipse.org/projects/handbook/#release) of the Eclipse project handbook which discusses _Major_, _Minor_, and _Service_ release criteria.
It is possible that these release categories align align with changes to the three version parts, but this is not explicitly stated in either `CycloneDDS` documentation or in the Eclipse project handbook.

### Version Stability [1.ii]

`CycloneDDS` is at a stable version. The current version can be found in its [package.xml](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/package.xml), and its change history can be found in its [CHANGELOG](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/CHANGELOG.rst).

### Public API Declaration [1.iii]

All symbols in the installed headers are considered part of the public API. In the source repository, these header files reside with each of the modules that make up CycloneDDS.

### API Stability Policy [1.iv]

`CycloneDDS` will not break public API within a released ROS distribution, i.e. no major releases once the ROS distribution is released. It conforms to the [Releases section](https://www.eclipse.org/projects/handbook/#release) of the Eclipse project handbook which states that releases which include breaking API changes are considered "Major".

### ABI Stability Policy [1.v]

`CycloneDDS` provides ABI stability for PATCH release. `CycloneDDS` strives to provide ABI stability for MINOR release. `CycloneDDS` not guarantee ABI stability for MAJOR release.

### ABI and ABI Stability Within a Released ROS Distribution [1.vi]

`CycloneDDS` will not break API nor ABI within a released ROS distribution, i.e. no major releases once the ROS distribution is released. 
As an external package, `CycloneDDS` is not released on the same cadence as ROS.
Changes to the branch of the `CycloneDDS` repository that is targeted by a given ROS release would be picked up by development builds of that ROS release.

## Change Control Process [2]

`CycloneDDS` follows the recommended guidelines of the Eclipse Development Process.

For the RMW layer, we follow the ROS core packages process. For Eclipse Cyclone, we ensure the stability within the project through review, CI and tests and additionally run ROS CI for changes that are likely to affect ROS.

All commits must be signed by the author and there must be an Eclipse Contributor Agreement on file with the Eclipse Foundation.

Pull requests are required to pass all tests in the CI system, unless Committers consider there is sufficient evidence that a failure is the result of a mishap unrelated to the change. Pull requests are only merged if the Committers deem it of acceptable quality and provide sufficient coverage of new functionality or proof of a bug fix via tests.

Only the Committers have write access to the repository and they are voted for in elections monitored by the Eclipse Foundation staff.

### Change Requests [2.i]

All changes will occur through a pull request, check ROS 2 Developer Guide for additional information.

### Contributor Origin [2.ii]

This package uses DCO as its confirmation of contributor origin policy. More information can be found in [CONTRIBUTING](https://www.eclipse.org/legal/DCO.php).

### Peer Review Policy [2.iii]

All pull requests will be peer-reviewed, check [Eclipse Developer Process](https://www.eclipse.org/projects/dev_process/) for additional information.

### Continuous Integration [2.iv]

All pull requests must pass CI on all tier 1 platforms
Currently nightly results can be seen here:
* [linux-aarch64_release](https://ci.ros2.org/view/nightly/job/nightly_linux-aarch64_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [linux_release](https://ci.ros2.org/view/nightly/job/nightly_linux_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [mac_osx_release](https://ci.ros2.org/view/nightly/job/nightly_osx_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [windows_release](https://ci.ros2.org/view/nightly/job/nightly_win_rel/lastBuild/testReport/rmw_cyclonedds_cpp/)

Incoming pull requests automatically trigger continuous integration testing and must run successfully to be merged.
Automated testing runs for:
- Ubuntu Xenial with gcc 8 and Clang 7.0.0
- macOS Mojave with Xcode 11.1
- macOS Sierra with Xcode 9
- Windows Server semi-annual release with Visual Studio 2017

### Documentation Policy [2.v]
All pull requests must resolve related documentation changes before merging.

## Documentation [3]

### Feature Documentation [3.i]

[Project documentation](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/docs/dev/modules.md#feature-discovery) states that the features available in the product are "largely dynamic" based on compile-time discovery.
`CycloneDDS` documentation covers all of the stable interface, and PRs that add to it need to include documentation. 
An explicit list of those features, and what criteria is required for discovery, is unavailable.

### Public API Documentation [3.ii]

The repository includes a [section](https://github.com/eclipse-cyclonedds/cyclonedds#documentation) discussing documentation which states that there is currently only limited documentation.
Generated documentation for the API is available in the [PDF document](https://raw.githubusercontent.com/eclipse-cyclonedds/cyclonedds/assets/pdf/CycloneDDS-0.1.0.pdf) linked in the project README.

### License [3.iii]

The license for `CycloneDDS` is the Eclipse Public License 2.0 and the Eclipse Distribution License 1.0, and all of the code includes a header stating so.
The project includes a [`NOTICE`](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/NOTICE.md#declared-project-licenses) with links to more information about these licenses.
The `CycloneDDS` repository also includes a [`LICENSE`](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/LICENSE) file with the full terms.

There is some third-party content included with `CycloneDDS` which is licensed as Zlib, New BSD, and Public Domain.
Details can also be found in the included [`NOTICE`](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/NOTICE.md#third-party-content) document.

### Copyright Statement [3.iv]

The `CycloneDDS` documentation includes a [policy](https://github.com/eclipse-cyclonedds/cyclonedds/blob/master/NOTICE.md#copyright) regarding content copyright, each of the source files containing code include a copyright statement with the license information in the file's header.

## Testing [4]

Some directories within the `CycloneDDS` source tree contain subdirectories for test code.
In all, the test code appears to comprise approximately 25% of the codebase.

### Feature Testing [4.i]

Each feature in `CycloneDDS` has corresponding tests which simulate typical usage, and they are located in separate directories next to the sources. New features are required to have tests before being added.
Currently nightly results can be seen here:
* [linux-aarch64_release](https://ci.ros2.org/view/nightly/job/nightly_linux-aarch64_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [linux_release](https://ci.ros2.org/view/nightly/job/nightly_linux_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [mac_osx_release](https://ci.ros2.org/view/nightly/job/nightly_osx_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [windows_release](https://ci.ros2.org/view/nightly/job/nightly_win_rel/lastBuild/testReport/rmw_cyclonedds_cpp/)

A substantial amount of the tests found throughout the source tree appear to verify functionality of various features of `CycloneDDS`.
However the lack of a complete feature list (see section [3.i]) makes it difficult to analyze the breadth of the tests.

### Public API Testing [4.ii]

Each part of the public API has tests, and new additions or changes to the public API require tests before being added. The tests aim to cover both typical usage and corner cases, but are quantified by contributing to code coverage.
There are some tests throughout the `CycloneDDS` source tree which specifically target the public API, but there are no policies or mechanisms to discover and measure which tests target the public API or how much of the public API is covered by the existing tests.

### Coverage [4.iii]

There is no test coverage tracking in `CycloneDDS`. Automated coverage runs are being added to the CI to show coverage.


### Performance [4.iv]

`CycloneDDS` performance is verifiably good and regression free per ROS Tooling WG's [nightly CI performance tests](http://build.ros2.org/job/Fci__nightly-performance_ubuntu_focal_amd64/ ).
Though the `CycloneDDS` [documentation](https://github.com/eclipse-cyclonedds/cyclonedds#performance) discusses the product's performance and discusses what metrics describe it, very few tests seem to validate the given statistics or ensure that the performance does not regress.
One of the [example projects](https://github.com/eclipse-cyclonedds/cyclonedds/blob/15e68152c9d14105e87ab1afc7e5af9c9589f776/examples/throughput/readme.rst) can be used to measure the throughput of the product, but does not provide a mechanism for analyzing resource usage or latency.

### Linters and Static Analysis [4.v]
`CycloneDDS` uses and passes all the ROS2 standard linters and static analysis tools for a C++ package as described in the [ROS 2 Developer Guide](https://index.ros.org/doc/ros2/Contributing/Developer-Guide/#linters-and-static-analysis). Passing implies there are no linter/static errors when testing against CI of supported platforms.
Currently nightly results can be seen here:
* [linux-aarch64_release](https://ci.ros2.org/view/nightly/job/nightly_linux-aarch64_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [linux_release](https://ci.ros2.org/view/nightly/job/nightly_linux_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [mac_osx_release](https://ci.ros2.org/view/nightly/job/nightly_osx_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [windows_release](https://ci.ros2.org/view/nightly/job/nightly_win_rel/lastBuild/testReport/rmw_cyclonedds_cpp/)

`CycloneDDS` has automated daily [Synopsys Coverity static code analysis](https://www.synopsys.com/software-integrity/security-testing/static-analysis-sast.html) with public results that can be seen [here](https://scan.coverity.com/projects/eclipse-cyclonedds-cyclonedds). `CycloneDDS` defect density is 0.05 per 1,000 lines of code as of Aug 11th 2020. For comparison the average defect density of open source software projects of similar size is 0.5.
In continuous integration, ASAN is enabled for some of the test matrix. The CI run includes address sanitizer runs, ergo, no PRs can be accepted that are not clean with respect to the address sanitizer.
There do not appear to be any linters enabled for the `CycloneDDS` repository.

## Dependencies [5]

### Direct Runtime ROS Dependencies [5.i]

As an external dependency, there are no ROS dependencies in `CycloneDDS`.

### Optional Direct Runtime ROS Dependencies [5.ii]

As an external dependency, there are no ROS dependencies in `CycloneDDS`.

### Direct Runtime non-ROS Dependency [5.iii]

The only runtime dependency of `CycloneDDS` is `OpenSSL`, a widely-used secure communications suite.
If `CycloneDDS` is built without security enabled, the product has no apparent runtime dependencies.

## Platform Support [6]

`CycloneDDS` supports all of the tier 1 platforms as described in REP-2000, and tests each change against all of them.

Currently nightly results can be seen here:
* [linux-aarch64_release](https://ci.ros2.org/view/nightly/job/nightly_linux-aarch64_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [linux_release](https://ci.ros2.org/view/nightly/job/nightly_linux_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [mac_osx_release](https://ci.ros2.org/view/nightly/job/nightly_osx_release/lastBuild/testReport/rmw_cyclonedds_cpp/)
* [windows_release](https://ci.ros2.org/view/nightly/job/nightly_win_rel/lastBuild/testReport/rmw_cyclonedds_cpp/)

## Security [7]

### Vulnerability Disclosure Policy [7.i]

This package conforms to the Vulnerability Disclosure Policy in REP-2006. The Eclipse Project Handbook states the project's vulnerability disclosure policy in detail.The Eclipse Project Handbook states the project's [vulnerability disclosure policy](https://www.eclipse.org/projects/handbook/#vulnerability-disclosure) in detail.
